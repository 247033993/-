<h1 id="toc_0">manifestPlaceholders</h1>

<h3 id="toc_1">利用manifestPlaceholders</h3>

<p>在项目中，我们有时会需要根据不同的项目环境，使用不同的项目变量，比如说，我在测试环境中需要我的app访问的服务器地址是测试服务器上，而正式发布下的app需要访问正式服务器。在这种情况下，我们可以将这个变量放在AndroidManifest文件中，根据不同的编译类型生成服务器指向不同的app</p>

<p>在新版本的gradle中，processManifest这个方法被移除掉了，而提供了一个新的功能manifestPlaceholders，我们可以在AndroidManifest中定义一个变量，在build.gradle中动态的替换掉，十分方便，语法也十分简单。例如，我们需要动态替换友盟的appkey，需要在AndroidManifest中定义一个变量</p>

<div><pre><code class="language-none">&lt;meta-data
     android:name=&quot;UMENG_APPKEY&quot;
     android:value=&quot;${umeng_app_key}&quot;/&gt;</code></pre></div>

<p>接着，我们在build.gradle文件中根据不同的环境，生成不同appkey的apk。</p>

<div><pre><code class="language-none">buildTypes {
    debug {
     manifestPlaceholders = [umeng_app_key: &quot;你替代的内容&quot;]
    }
    release {
 　　manifestPlaceholders = [umeng_app_key: &quot;你替代的内容&quot;]
    }
    develop {
　　 manifestPlaceholders = [umeng_app_key: &quot;你替代的内容&quot;]
    }
}</code></pre></div>

<p>运行gralde clean build，你就可以生成不同的appkey的apk，是不是感觉好多了。^ ^</p>

<p>如果你想要替换多个变量，假如你需要两个变量要替换，需要按照下面形式进行</p>

<div><pre><code class="language-none">&lt;meta-data
     android:name=&quot;UMENG_APPKEY&quot;
     android:value=&quot;${umeng_app_key}&quot;/&gt;
&lt;meta-data
      android:name=&quot;UMENG_SECRET&quot;
android:value=&quot;${umeng_app_secret}&quot;/&gt;
buildTypes {
    debug {
manifestPlaceholders = [umeng_app_key: &quot;你替代的内容&quot;,umeng_app_secret:&quot;你要替换的内容&quot;]
    }
    ...
}</code></pre></div>
