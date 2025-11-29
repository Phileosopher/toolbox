
# reference and cheatsheets

## StarPlane game proof of concept tools

[StarPlane game proof of concept](https://gist.github.com/JohnSundell/7ae3223b5bad3712378a57aaff31d7e2)
[John Sundell on X: "Can SwiftUI be used to build a game? This is StarPlane - a game written in SwiftUI, using SFSymbols for graphics This is just a fun little thing that I quickly hacked together, not a serious project Source code here: https://t.co/3vJl0nVS1i https://t.co/OPctJJK8cF" / X](https://twitter.com/johnsundell/status/1280998529394184193)

### Swift code (StarPlane.swift)

// A fun little game written in SwiftUI
// Copyright (c) John Sundell 2020, MIT license.
// This is a hacky implementation written just for fun.
// It's only verified to work on iPhones in portrait mode.

import SwiftUI

final class GameController: ObservableObject {
    @Published var plane = GameObject.plane()
    @Published private(set) var clouds = [GameObject]()
    @Published private(set) var stars = [GameObject]()
    @Published private(set) var score = 0
    var movement: Movement?
    private var lastCloudSpawnDate = Date()
    private var lastStarSpawnDate = Date()
    private var displayLink: CADisplayLink?

    func activate() {
        guard displayLink == nil else { return }

        let link = CADisplayLink(target: self, selector: #selector(update))
        link.preferredFramesPerSecond = 60
        link.add(to: .main, forMode: .common)
        displayLink = link
    }

    @objc private func update() {
        switch movement?.direction {
        case nil:
            break
        case .leading:
            plane.offset.x -= plane.speed
        case .trailing:
            plane.offset.x += plane.speed
        }

        plane.offset.x = max(0.1, min(plane.offset.x, 0.9))

        let currentDate = Date()

        if currentDate.timeIntervalSince(lastCloudSpawnDate) > 1.5 {
            clouds.append(.cloud())
            lastCloudSpawnDate = currentDate
        }

        if currentDate.timeIntervalSince(lastStarSpawnDate) > 3 {
            stars.append(.star())
            lastStarSpawnDate = currentDate
        }

        moveGameObjects(\.clouds)
        moveGameObjects(\.stars)

        let collisionThreshold: CGFloat = 0.06

        stars = stars.filter { star in
            let contact = (
                x: abs(plane.offset.x - star.offset.x) < collisionThreshold,
                y: abs(plane.offset.y - star.offset.y) < collisionThreshold
            )

            guard contact.x, contact.y else {
                return true
            }

            score += 100
            return false
        }
    }

    private func moveGameObjects(
        _ keyPath: ReferenceWritableKeyPath<GameController, [GameObject]>
    ) {
        self[keyPath: keyPath] = self[keyPath: keyPath].compactMap {
            var object = $0
            object.offset.y += object.speed
            return object.offset.y < 1.1 ? object : nil
        }
    }
}

struct Movement {
    enum Direction {
        case leading, trailing
    }

    var direction: Direction? = nil
    var location: CGPoint
}

struct Game: View {
    @ObservedObject var controller: GameController

    var body: some View {
        GeometryReader { proxy in
            ForEach(controller.clouds) { cloud in
                cloud.renderedInContainer(ofSize: proxy.size)
            }
            ForEach(controller.stars) { star in
                star.renderedInContainer(ofSize: proxy.size)
            }
            ZStack(alignment: .top) {
                HStack {
                    Spacer()
                    Text("Score: \(controller.score)")
                        .bold()
                        .foregroundColor(.black)
                    Spacer()
                }
                .padding(.top)
            }
            controller.plane
                .renderedInContainer(ofSize: proxy.size)
        }
        .background(Color(#colorLiteral(red: 0, green: 0.7216904445, blue: 1, alpha: 1)).edgesIgnoringSafeArea(.all))
        .onAppear(perform: controller.activate)
        .gesture(gesture)
    }

    private var gesture: some Gesture {
        DragGesture(minimumDistance: 0)
            .onChanged { state in
                guard var movement = controller.movement else {
                    controller.movement = Movement(location: state.location)
                    return
                }

                let delta = state.location.x - movement.location.x
                let threshold: CGFloat = 5

                if delta > threshold {
                    movement.direction = .trailing
                } else if delta < -threshold {
                    movement.direction = .leading
                }

                movement.location = state.location
                controller.movement = movement
            }
            .onEnded { _ in
                controller.movement = nil
            }
    }
}

struct GameObject: View, Identifiable {
    let id = UUID()
    var spriteName: String
    var color: Color
    var speed: CGFloat
    var scale: CGFloat
    var rotation = Angle(degrees: 0)
    var offset = Self.randomStartOffset()

    var body: some View {
        Image(systemName: spriteName)
            .resizable()
            .aspectRatio(contentMode: .fit)
            .foregroundColor(color)
            .rotationEffect(rotation)
    }

    func renderedInContainer(ofSize size: CGSize) -> some View {
        position(
            x: offset.x * size.width,
            y: offset.y * size.height
        )
        .frame(width: size.width * scale)
    }
}

extension GameObject {
    static func plane() -> Self {
        GameObject(
            spriteName: "airplane",
            color: .black,
            speed: 0.005,
            scale: 0.1,
            rotation: Angle(degrees: -90),
            offset: (0.5, 0.9)
        )
    }

    static func cloud() -> Self {
        GameObject(
            spriteName: "icloud.fill",
            color: .white,
            speed: 0.002,
            scale: 0.3
        )
    }

    static func star() -> Self {
        GameObject(
            spriteName: "star.fill",
            color: .yellow,
            speed: 0.005,
            scale: 0.1
        )
    }

    private static func randomStartOffset() -> (x: CGFloat, y: CGFloat) {
        (.random(in: 0..<1), -0.1)
    }
}
