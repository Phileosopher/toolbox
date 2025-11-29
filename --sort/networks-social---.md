
# reference and cheatsheets

## specific social media - Discord - delete messages (can get account banned).txt
/**
 * @name QuickDeleteMessages
 * @description Hold delete and click a message to delete it quickly.
 * @author 1Lighty
 * @authorId 239513071272329217
 * @version 1.0.12
 * @invite NYvWdN5
 * @donate https://paypal.me/lighty13
 * @updateUrl https://gitlab.com/_Lighty_/bdstuff/-/raw/master/public/plugins/QuickDeleteMessages.plugin.js
 */
/*@cc_on
@if (@_jscript)

  // Offer to self-install for clueless users that try to run this directly.
  var shell = WScript.CreateObject('WScript.Shell');
  var fs = new ActiveXObject('Scripting.FileSystemObject');
  var pathPlugins = shell.ExpandEnvironmentStrings('%APPDATA%\\BetterDiscord\\plugins');
  var pathSelf = WScript.ScriptFullName;
  // Put the user at ease by addressing them in the first person
  shell.Popup('It looks like you\'ve mistakenly tried to run me directly. \n(Don\'t do that!)', 0, 'I\'m a plugin for BetterDiscord', 0x30);
  if (fs.GetParentFolderName(pathSelf) === fs.GetAbsolutePathName(pathPlugins)) {
    shell.Popup('I\'m in the correct folder already.\nJust go to settings, plugins and enable me.', 0, 'I\'m already installed', 0x40);
  } else if (!fs.FolderExists(pathPlugins)) {
    shell.Popup('I can\'t find the BetterDiscord plugins folder.\nAre you sure it\'s even installed?', 0, 'Can\'t install myself', 0x10);
  } else if (shell.Popup('Should I copy myself to BetterDiscord\'s plugins folder for you?', 0, 'Do you need some help?', 0x34) === 6) {
    fs.CopyFile(pathSelf, fs.BuildPath(pathPlugins, fs.GetFileName(pathSelf)), true);
    // Show the user where to put plugins in the future
    shell.Exec('explorer ' + pathPlugins);
    shell.Popup('I\'m installed!\nJust go to settings, plugins and enable me!', 0, 'Successfully installed', 0x40);
  }
  WScript.Quit();

@else@*/
/*
 * Copyright Â© 2019-2020, _Lighty_
 * All rights reserved.
 * Code may not be redistributed, modified or otherwise taken without explicit permission.
 */
module.exports = (() => {
  /* Setup */
  const config = {
    main: 'index.js',
    info: {
      name: 'QuickDeleteMessages',
      authors: [
        {
          name: 'Lighty',
          discord_id: '239513071272329217',
          github_username: 'LightyPon',
          twitter_username: ''
        }
      ],
      version: '1.0.12',
      description: 'Hold delete and click a message to delete it quickly.',
      github: 'https://github.com/1Lighty',
      github_raw: 'https://gitlab.com/_Lighty_/bdstuff/-/raw/master/public/plugins/QuickDeleteMessages.plugin.js'
    },
    changelog: [
      {
        title: 'Fixed',
        type: 'added',
        items: ['Fixed plugin being non functional.']
      }
    ],
    defaultConfig: [
      {
        type: 'category',
        id: 'misc',
        name: 'settings',
        collapsible: true,
        shown: true,
        settings: [
          {
            name: 'Show confirmation',
            note: 'Can still hold shift to bypass it!',
            id: 'confirmDelete',
            type: 'switch',
            value: false
          },
          {
            name: 'Use CTRL instead of Delete',
            id: 'ctrlClickDelete',
            type: 'switch',
            value: false
          }
        ]
      }
    ]
  };

  /* Build */
  const buildPlugin = ([Plugin, Api]) => {
    const { ContextMenu, EmulatedTooltip, Toasts, Settings, Popouts, Modals, Utilities, WebpackModules, Filters, DiscordModules, ColorConverter, DOMTools, DiscordClasses, DiscordSelectors, ReactTools, ReactComponents, Logger, Patcher, PluginUpdater, PluginUtilities, DiscordClassModules, Structs } = Api;
    const { React, ModalStack, ContextMenuActions, ContextMenuItem, ContextMenuItemsGroup, ReactDOM, ChannelStore, GuildStore, UserStore, DiscordConstants, Dispatcher, GuildMemberStore, GuildActions, SwitchRow, EmojiUtils, RadioGroup, FlexChild, PopoutOpener, Textbox } = DiscordModules;

    const Permissions = WebpackModules.getByProps('can', 'initialize');

    const cssPath = function(el) {
      if (!(el instanceof Element)) return;
      const path = [];
      while (el.nodeType === Node.ELEMENT_NODE) {
        let selector = el.nodeName.toLowerCase();
        if (el.id) selector += `#${el.id}`;
        else {
          let sib = el, nth = 1;
          while (sib.nodeType === Node.ELEMENT_NODE && (sib = sib.previousSibling) && nth++);
          selector += `:nth-child(${nth})`;
        }
        path.unshift(selector);
        el = el.parentNode;
        if (el.id === 'app-mount') break;
      }
      return path.join(' > ');
    };

    return class QuickDeleteMessages extends Plugin {
      constructor() {
        super();
        try {
          WebpackModules.getByProps('openModal', 'hasModalOpen').closeModal(`${this.name}_DEP_MODAL`);
        } catch (e) { }
      }
      onStart() {
        this.tools = {
          deleteMessage: DiscordModules.MessageActions.deleteMessage,
          confirmDelete: WebpackModules.getByProps('confirmDelete').confirmDelete
        };

        this.deleteKeyDown = false;
        document.addEventListener(
          'keydown',
          (this.keydownListener = e => {
            if (e.repeat) return;
            if (e.keyCode === 46) this.deleteKeyDown = true;
          })
        );
        document.addEventListener(
          'keyup',
          (this.keyupListener = e => {
            if (e.repeat) return;
            if (e.keyCode === 46) this.deleteKeyDown = false;
          })
        );
        const messageClassname = WebpackModules.getByProps('groupStart', 'message').message.split(' ')[0];
        const containerClassname = WebpackModules.getByProps('embedWrapper', 'container').container.split(' ')[0];
        document.addEventListener(
          'click',
          (this.clickListener = e => {
            if (this.settings.misc.ctrlClickDelete ? !e.ctrlKey : !this.deleteKeyDown) return;
            let { target } = e;
            while (target && (!target.classList || !target.classList.contains(messageClassname))) target = target.parentElement;
            if (!target) return;
            const instance = ReactTools.getOwnerInstance(document.querySelector(cssPath(target.querySelector(`.${ containerClassname}`))));
            if (!instance || !instance.props || !instance.props.message) return;
            if (!this.canDelete(instance.props)) return;
            this.settings.misc.confirmDelete && !e.shiftKey ? this.tools.confirmDelete(instance.props.channel, instance.props.message, true) : this.tools.deleteMessage(instance.props.channel.id, instance.props.message.id);
            e.preventDefault();
            e.stopPropagation();
            return false;
          }),
          true
        );
      }

      onStop() {
        if (this.keydownListener) document.removeEventListener('keydown', this.keydownListener);
        if (this.keyupListener) document.removeEventListener('keyup', this.keyupListener);
        if (this.clickListener) document.removeEventListener('click', this.clickListener);
      }

      canDelete(props) {
        return props.message.author.id === UserStore.getCurrentUser().id || Permissions.can(DiscordModules.DiscordPermissions.MANAGE_MESSAGES, props.channel);
      }

      /* zlib uses reference to defaultSettings instead of a cloned object, which sets settings as default settings, messing everything up */
      loadSettings(defaultSettings) {
        return PluginUtilities.loadSettings(this.name, Utilities.deepclone(this.defaultSettings ? this.defaultSettings : defaultSettings));
      }

      /* PATCHES */

      patchAll() { }

      /* PATCHES */

      getSettingsPanel() {
        return this.buildSettingsPanel().getElement();
      }

      get [Symbol.toStringTag]() {
        return 'Plugin';
      }
      get css() {
        return this._css;
      }
      get name() {
        return config.info.name;
      }
      get short() {
        let string = '';

        for (let i = 0, len = config.info.name.length; i < len; i++) {
          const char = config.info.name[i];
          if (char === char.toUpperCase()) string += char;
        }

        return string;
      }
      get author() {
        return config.info.authors.map(author => author.name).join(', ');
      }
      get version() {
        return config.info.version;
      }
      get description() {
        return config.info.description;
      }
    };
  };

  /* Finalize */

  let ZeresPluginLibraryOutdated = false;
  try {
    if (global.BdApi && BdApi.Plugins && typeof BdApi.Plugins.get === 'function') {
      const a = (c, a) => ((c = c.split('.').map(b => parseInt(b))), (a = a.split('.').map(b => parseInt(b))), !!(a[0] > c[0])) || !!(a[0] == c[0] && a[1] > c[1]) || !!(a[0] == c[0] && a[1] == c[1] && a[2] > c[2]),
        b = BdApi.Plugins.get('ZeresPluginLibrary');
      ((b, c) => b && b._config && b._config.info && b._config.info.version && a(b._config.info.version, c))(b, '1.2.18') && (ZeresPluginLibraryOutdated = !0);
    }
  } catch (e) {
    console.error('Error checking if ZeresPluginLibrary is out of date', e);
  }

  return !global.ZeresPluginLibrary || ZeresPluginLibraryOutdated
    ? class {
      constructor() {
        this._config = config;
        this.start = this.load = this.handleMissingLib;
      }
      getName() {
        return this.name.replace(/\s+/g, '');
      }
      getAuthor() {
        return this.author;
      }
      getVersion() {
        return this.version;
      }
      getDescription() {
        return `${this.description } You are missing ZeresPluginLibrary for this plugin, please enable the plugin and click Download Now.`;
      }
      stop() { }
      start() {
        this.handleMissingLib();
      }
      load() {
        this.handleMissingLib();
      }
      handleMissingLib() {
        const a = BdApi.findModuleByProps('openModal', 'hasModalOpen');
        if (a && a.hasModalOpen(`${this.name}_DEP_MODAL`)) return;
        const b = !global.ZeresPluginLibrary,
          c = ZeresPluginLibraryOutdated ? 'Outdated Library' : 'Missing Library',
          d = `The Library ZeresPluginLibrary required for ${this.name} is ${ZeresPluginLibraryOutdated ? 'outdated' : 'missing'}.`,
          e = BdApi.findModuleByDisplayName('Text'),
          f = BdApi.findModuleByDisplayName('ConfirmModal'),
          g = () => BdApi.alert(c, BdApi.React.createElement('span', {}, BdApi.React.createElement('div', {}, d), 'Due to a slight mishap however, you\'ll have to download the libraries yourself. This is not intentional, something went wrong, errors are in console.', b || ZeresPluginLibraryOutdated ? BdApi.React.createElement('div', {}, BdApi.React.createElement('a', { href: 'https://betterdiscord.net/ghdl?id=2252', target: '_blank' }, 'Click here to download ZeresPluginLibrary')) : null));
        if (!a || !f || !e) return console.error(`Missing components:${(a ? '' : ' ModalStack') + (f ? '' : ' ConfirmationModalComponent') + (e ? '' : 'TextElement')}`), g();
        class h extends BdApi.React.PureComponent {
          constructor(a) {
            super(a), (this.state = { hasError: !1 });
          }
          componentDidCatch(a) {
            console.error(`Error in ${this.props.label}, screenshot or copy paste the error above to Lighty for help.`), this.setState({ hasError: !0 }), typeof this.props.onError === 'function' && this.props.onError(a);
          }
          render() {
            return this.state.hasError ? null : this.props.children;
          }
        }
        let i = !1,
          j = !1;
        const k = a.openModal(
          b => {
            if (j) return null;
            try {
              return BdApi.React.createElement(
                h,
                {
                  label: 'missing dependency modal',
                  onError: () => {
                    a.closeModal(k), g();
                  }
                },
                BdApi.React.createElement(
                  f,
                  {
                    header: c,
                    children: BdApi.React.createElement(e, { size: e.Sizes.SIZE_16, children: [`${d} Please click Download Now to download it.`] }),
                    red: !1,
                    confirmText: 'Download Now',
                    cancelText: 'Cancel',
                    onCancel: b.onClose,
                    onConfirm: () => {
                      if (i) return;
                      i = !0;
                      const b = require('request'),
                        c = require('fs'),
                        d = require('path');
                      b('https://raw.githubusercontent.com/rauenzi/BDPluginLibrary/master/release/0PluginLibrary.plugin.js', (b, e, f) => {
                        try {
                          if (b || e.statusCode !== 200) return a.closeModal(k), g();
                          c.writeFile(d.join(BdApi.Plugins && BdApi.Plugins.folder ? BdApi.Plugins.folder : window.ContentManager.pluginsFolder, '0PluginLibrary.plugin.js'), f, () => { });
                        } catch (b) {
                          console.error('Fatal error downloading ZeresPluginLibrary', b), a.closeModal(k), g();
                        }
                      });
                    },
                    ...b,
                    onClose: () => { }
                  }
                )
              );
            } catch (b) {
              return console.error('There has been an error constructing the modal', b), (j = !0), a.closeModal(k), g(), null;
            }
          },
          { modalKey: `${this.name}_DEP_MODAL` }
        );
      }
      get [Symbol.toStringTag]() {
        return 'Plugin';
      }
      get name() {
        return config.info.name;
      }
      get short() {
        let string = '';
        for (let i = 0, len = config.info.name.length; i < len; i++) {
          const char = config.info.name[i];
          if (char === char.toUpperCase()) string += char;
        }
        return string;
      }
      get author() {
        return config.info.authors.map(author => author.name).join(', ');
      }
      get version() {
        return config.info.version;
      }
      get description() {
        return config.info.description;
      }
    }
    : buildPlugin(global.ZeresPluginLibrary.buildPlugin(config));
})();

/*@end@*/
