---
id: upgrading
title: upgrading
---
<a id="content"></a><h1><a class="anchor" name="upgrading-to-new-react-native-versions"></a>Upgrading to new React Native versions <a class="hash-link" href="docs/upgrading.html#upgrading-to-new-react-native-versions">#</a></h1><div><p>Upgrading to new versions of React Native will give you access to more APIs, views, developer tools and other goodies. Upgrading requires a small amount of effort, but we try to make it easy for you. The instructions are a bit different depending on whether you used <code>create-react-native-app</code> or <code>react-native init</code> to create your project.</p><h2><a class="anchor" name="create-react-native-app-projects"></a>Create React Native App projects <a class="hash-link" href="docs/upgrading.html#create-react-native-app-projects">#</a></h2><p>Upgrading your Create React Native App project to a new version of React Native requires updating the <code>react-native</code>, <code>react</code>, and <code>expo</code> package versions in your <code>package.json</code> file. Please refer to <a href="https://github.com/react-community/create-react-native-app/blob/master/VERSIONS.md" target="_blank">this document</a> to find out what versions are supported. You will also need to set the correct <code>sdkVersion</code> in your <code>app.json</code> file.</p><p>See the <a href="https://github.com/react-community/create-react-native-app/blob/master/react-native-scripts/template/README.md#updating-to-new-releases" target="_blank">CRNA user guide</a> for up-to-date information about upgrading your project.</p><h2><a class="anchor" name="projects-built-with-native-code"></a>Projects built with native code <a class="hash-link" href="docs/upgrading.html#projects-built-with-native-code">#</a></h2><span><div class="banner-crna-ejected">
  <h3>Projects with Native Code Only</h3>
  <p>
    This section only applies to projects made with <code>react-native init</code> or to those made with Create React Native App which have since ejected. For more information about ejecting, please see the <a href="https://github.com/react-community/create-react-native-app/blob/master/EJECTING.md" target="_blank">guide</a> on the Create React Native App repository.
  </p>
</div>

</span><p>Because React Native projects built with native code are essentially made up of an Android project, an iOS project, and a JavaScript project, upgrading can be rather tricky. Here's what you need to do to upgrade from an older version of React Native.</p><h3><a class="anchor" name="upgrade-based-on-git"></a>Upgrade based on Git <a class="hash-link" href="docs/upgrading.html#upgrade-based-on-git">#</a></h3><p>The module <code>react-native-git-upgrade</code> provides a one-step operation to upgrade the source files with a minimum of conflicts. Under the hood, it consists in 2 phases:</p><ul><li>First, it computes a Git patch between both old and new template files,</li><li>Then, the patch is applied on the user's sources.</li></ul><blockquote><p><strong>IMPORTANT:</strong> You don't have to install the new version of the <code>react-native</code> package, it will be installed automatically.</p></blockquote><h4><a class="anchor" name="1-install-git"></a>1. Install Git <a class="hash-link" href="docs/upgrading.html#1-install-git">#</a></h4><p>While your project does not have to be handled by the Git versioning system -- you can use Mercurial, SVN, or nothing -- you will still need to <a href="https://git-scm.com/downloads" target="_blank">install Git</a> on your system in order to use <code>react-native-git-upgrade</code>. Git will also need to be available in the <code>PATH</code>.</p><h4><a class="anchor" name="2-install-the-react-native-git-upgrade-module"></a>2. Install the <code>react-native-git-upgrade</code> module <a class="hash-link" href="docs/upgrading.html#2-install-the-react-native-git-upgrade-module">#</a></h4><p>The <code>react-native-git-upgrade</code> module provides a CLI and must be installed globally:</p><div class="prism language-sh">$ npm install <span class="token operator">-</span>g react<span class="token operator">-</span>native<span class="token operator">-</span>git<span class="token operator">-</span>upgrade</div><h4><a class="anchor" name="3-run-the-command"></a>3. Run the command <a class="hash-link" href="docs/upgrading.html#3-run-the-command">#</a></h4><p>Run the following command to start the process of upgrading to the latest version:</p><div class="prism language-sh">$ react<span class="token operator">-</span>native<span class="token operator">-</span>git<span class="token operator">-</span>upgrade</div><blockquote><p>You may specify a React Native version by passing an argument: <code>react-native-git-upgrade X.Y</code></p></blockquote><p>The templates are upgraded in a optimized way. You still may encounter conflicts but only where the Git 3-way merge have failed, depending on the version and how you modified your sources.</p><h4><a class="anchor" name="4-resolve-the-conflicts"></a>4. Resolve the conflicts <a class="hash-link" href="docs/upgrading.html#4-resolve-the-conflicts">#</a></h4><p>Conflicted files include delimiters which make very clear where the changes come from. For example:</p><div class="prism language-javascript">13B07F951A680F5B00A75B9A <span class="token comment" spellcheck="true">/* Release */</span> <span class="token operator">=</span> <span class="token punctuation">{</span>
  isa <span class="token operator">=</span> XCBuildConfiguration<span class="token punctuation">;</span>
  buildSettings <span class="token operator">=</span> <span class="token punctuation">{</span>
    ASSETCATALOG_COMPILER_APPICON_NAME <span class="token operator">=</span> AppIcon<span class="token punctuation">;</span>
<span class="token operator">&lt;&lt;</span><span class="token operator">&lt;&lt;</span><span class="token operator">&lt;&lt;</span><span class="token operator">&lt;</span> ours
    CODE_SIGN_IDENTITY <span class="token operator">=</span> <span class="token string">"iPhone Developer"</span><span class="token punctuation">;</span>
    FRAMEWORK_SEARCH_PATHS <span class="token operator">=</span> <span class="token punctuation">(</span>
      <span class="token string">"$(inherited)"</span><span class="token punctuation">,</span>
      <span class="token string">"$(PROJECT_DIR)/HockeySDK.embeddedframework"</span><span class="token punctuation">,</span>
      <span class="token string">"$(PROJECT_DIR)/HockeySDK-iOS/HockeySDK.embeddedframework"</span><span class="token punctuation">,</span>
    <span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token operator">===</span><span class="token operator">===</span><span class="token operator">=</span>
    CURRENT_PROJECT_VERSION <span class="token operator">=</span> <span class="token number">1</span><span class="token punctuation">;</span>
<span class="token operator">&gt;&gt;&gt;</span><span class="token operator">&gt;&gt;&gt;</span><span class="token operator">&gt;</span> theirs
    HEADER_SEARCH_PATHS <span class="token operator">=</span> <span class="token punctuation">(</span>
      <span class="token string">"$(inherited)"</span><span class="token punctuation">,</span>
      <span class="token operator">/</span>Applications<span class="token operator">/</span>Xcode<span class="token punctuation">.</span>app<span class="token operator">/</span>Contents<span class="token operator">/</span>Developer<span class="token operator">/</span>Toolchains<span class="token operator">/</span>XcodeDefault<span class="token punctuation">.</span>xctoolchain<span class="token operator">/</span>usr<span class="token operator">/</span>include<span class="token punctuation">,</span>
      <span class="token string">"$(SRCROOT)/../node_modules/react-native/React/**"</span><span class="token punctuation">,</span>
      <span class="token string">"$(SRCROOT)/../node_modules/react-native-code-push/ios/CodePush/**"</span><span class="token punctuation">,</span>
    <span class="token punctuation">)</span><span class="token punctuation">;</span></div><p>You can think of "ours" as "your team" and "theirs" as "the React Native dev team".</p><h3><a class="anchor" name="alternative"></a>Alternative <a class="hash-link" href="docs/upgrading.html#alternative">#</a></h3><p>Use this only in case the above didn't work.</p><h4><a class="anchor" name="1-upgrade-the-react-native-dependency"></a>1. Upgrade the <code>react-native</code> dependency <a class="hash-link" href="docs/upgrading.html#1-upgrade-the-react-native-dependency">#</a></h4><p>Note the latest version of the <code>react-native</code> npm package <a href="https://www.npmjs.com/package/react-native" target="_blank">from here</a> (or use <code>npm info react-native</code> to check).</p><p>Now install that version of <code>react-native</code> in your project with <code>npm install --save</code>:</p><div class="prism language-sh">$ npm install <span class="token operator">--</span>save react<span class="token operator">-</span>native@X<span class="token punctuation">.</span>Y
# where X<span class="token punctuation">.</span>Y is the semantic version you are upgrading to
npm WARN peerDependencies The peer dependency react@<span class="token operator">~</span>R included <span class="token keyword">from</span> react<span class="token operator">-</span>native<span class="token operator">...</span></div><p>If you saw a warning about the peerDependency, also upgrade <code>react</code> by running:</p><div class="prism language-sh">$ npm install <span class="token operator">--</span>save react@R
# where R is the <span class="token keyword">new</span> <span class="token class-name">version</span> <span class="token keyword">of</span> react <span class="token keyword">from</span> the peerDependency warning you saw</div><h4><a class="anchor" name="2-upgrade-your-project-templates"></a>2. Upgrade your project templates <a class="hash-link" href="docs/upgrading.html#2-upgrade-your-project-templates">#</a></h4><p>The new npm package may contain updates to the files that are normally generated when you
run <code>react-native init</code>, like the iOS and the Android sub-projects.</p><p>You may consult <a href="https://github.com/ncuillery/rn-diff" target="_blank">rn-diff</a> to see if there were changes in the project template files.
In case there weren't any, simply rebuild the project and continue developing. In case of minor changes, you may update your project manually and rebuild.</p><p>If there were major changes, run this in a terminal to get these:</p><div class="prism language-sh">$ react<span class="token operator">-</span>native upgrade</div><p>This will check your files against the latest template and perform the following:</p><ul><li>If there is a new file in the template, it is simply created.</li><li>If a file in the template is identical to your file, it is skipped.</li><li>If a file is different in your project than the template, you will be prompted; you have options to keep your file or overwrite it with the template version.</li></ul><h2><a class="anchor" name="manual-upgrades"></a>Manual Upgrades <a class="hash-link" href="docs/upgrading.html#manual-upgrades">#</a></h2><p>Some upgrades require manual steps, e.g. 0.13 to 0.14, or 0.28 to 0.29. Be sure to check the <a href="https://github.com/facebook/react-native/releases" target="_blank">release notes</a> when upgrading so that you can identify any manual changes your particular project may require.</p></div><div class="docs-prevnext"><a class="docs-prev btn" href="docs/running-on-device.html#content">← Previous</a><a class="docs-next btn" href="docs/troubleshooting.html#content">Continue Reading →</a></div><p class="edit-page-block"><a target="_blank" href="https://github.com/facebook/react-native/blob/master/docs/Upgrading.md">Improve this page</a> by sending a pull request!</p>