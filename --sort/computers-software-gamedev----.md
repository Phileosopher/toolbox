
# reference and cheatsheets

## game ux-ui tools

[Game UI Database | Welcome](https://www.gameuidatabase.com/)
Game UI/UX Database

## Pong made with Swift Charts tools

[Pong made with Swift Charts](https://gist.github.com/dduan/a3ae008105950dbd843a32fa696a55e1)

### use the following Swift code (SwiftChartPong.swift)


import SwiftUI
import Charts
import Combine
import Foundation

final class GameState: ObservableObject {
    struct Player {
        var position: Int
        var halfSize: Int = 150

        var yStart: Int {
            position - halfSize
        }

        var yEnd: Int {
            position + halfSize
        }
    }

    let boardSize: Int = 1000
    var velocity: CGPoint = .zero
    let speed: CGFloat = 5
    var loser: String?
    var direction: CGFloat = .zero {
        didSet {
            self.velocity = .init(
                x: cos(self.direction) * self.speed,
                y: sin(self.direction) * self.speed
            )
        }
    }
    var cancels = Set<AnyCancellable>()

    init() {
        self.paused = true
        self.started = false
        self.p0 = .init(position: Int(boardSize / 2))
        self.p1 = .init(position: Int(boardSize / 2))
        self.ball = .init(x: boardSize / 2, y: boardSize / 2)
        Timer.publish(every: 0.013333333, on: .main, in: .common)
            .autoconnect()
            .sink { _ in
                self.update()
            }
            .store(in: &cancels)
    }

    func update() {
        guard !self.paused else {
            return
        }

        self.ball = .init(
            x: self.ball.x + self.velocity.x,
            y: self.ball.y + self.velocity.y
        )

        if ball.x < 0 || ball.x >= CGFloat(boardSize) {
            self.paused = true
            self.loser = ball.x < 0 ? "0" : "1"
            return
        }

        if ball.y >= CGFloat(boardSize) - 5 || ball.y <= 5 {
            self.direction = 2 * .pi - self.direction
        }

        if CGRect(
            x: 50,
            y: self.p0.yStart,
            width: 10,
            height: self.p0.halfSize * 2
        ).contains(ball)
        {
            let newDirection = (CGFloat(p0.position) - ball.y) / CGFloat(p0.halfSize) * (.pi / 1.8)
            self.direction = -newDirection
        }

        if CGRect(
            x: 940,
            y: self.p1.yStart,
            width: 10,
            height: self.p1.halfSize * 2
        ).contains(ball)
        {
            let newDirection = (CGFloat(p1.position) - ball.y) / CGFloat(p1.halfSize) * (.pi / 1.8)
            self.direction = newDirection - .pi
        }
    }

    @Published var started: Bool {
        didSet {
            self.paused = !started
            self.loser = nil
            if started {
                self.direction = Double.random(in: 0 ... .pi * 2)
            } else {
                self.p0 = .init(position: Int(boardSize / 2))
                self.p1 = .init(position: Int(boardSize / 2))
                self.ball = .init(x: boardSize / 2, y: boardSize / 2)
            }
        }
    }

    @Published var paused: Bool
    @Published var p0: Player
    @Published var p1: Player
    @Published var ball: CGPoint

    func moveP0(up: Bool) {
        self.p0.position = min(boardSize - self.p0.halfSize, max(self.p0.halfSize, self.p0.position + (up ? 50 : -50)))
    }

    func moveP1(up: Bool) {
        self.p1.position = min(boardSize - self.p1.halfSize, max(self.p1.halfSize, self.p1.position + (up ? 50 : -50)))
    }
}

struct ContentView: View {
    @StateObject var state = GameState()
    var body: some View {
        VStack {
            ZStack {
                ChartView(state: state)
                if let loser = state.loser {
                    Text("Player \(loser) is the loser!")
                }
            }
            Grid(horizontalSpacing: 5, verticalSpacing: 5) {
                GridRow {
                    Button(action: { state.moveP0(up: true) }) {
                        Text("⬆️").frame(width: 100, height: 100)
                    }
                    .buttonStyle(.bordered)
                    Button(action: { state.moveP1(up: true) }) {
                        Text("⬆️").frame(width: 100, height: 100)
                    }
                    .buttonStyle(.bordered)

                }
                GridRow {
                    Button(action: { state.moveP0(up: false) }) {
                        Text("⬇️").frame(width: 100, height: 100)
                    }
                    .buttonStyle(.bordered)
                    Button(action: { state.moveP1(up: false) }) {
                        Text("⬇️").frame(width: 100, height: 100)
                    }
                    .buttonStyle(.bordered)

                }

                GridRow {
                    Button(action: { state.started.toggle() }) {
                        Text(state.started ? "Reset" : "Start")
                            .frame(width: 100)
                    }
                    Button(action: { state.paused.toggle() }) {
                        Text(state.paused ? "Unpause" : "Pause")
                            .frame(width: 100)
                    }
                    .disabled(!state.started || state.loser != nil)
                }
                .buttonStyle(.borderedProminent)
            }
        }
    }
}

struct ChartView: View {
    @ObservedObject var state: GameState
    var body: some View {
        GeometryReader { geometry in
            Chart {
                PointMark(
                    x: .value("X", Int(state.ball.x)),
                    y: .value("Y", Int(state.ball.y))
                )
                .foregroundStyle(.red)
                BarMark(
                    x: .value("P0", 50),
                    yStart: .value("Y0", state.p0.yStart),
                    yEnd: .value("Y1", state.p0.yEnd)
                )
                BarMark(
                    x: .value("P1", 950),
                    yStart: .value("Y0", state.p1.yStart),
                    yEnd: .value("Y1", state.p1.yEnd)
                )
            }
            .chartXAxis(.hidden)
            .chartYAxis(.hidden)
            .chartYScale(domain: 0 ... state.boardSize)
            .chartXScale(domain: 0 ... state.boardSize)
            .chartPlotStyle { area in
                area.border(.black)
            }
            .padding()
            .frame(height: min(geometry.size.width, geometry.size.height))
        }
    }
}
