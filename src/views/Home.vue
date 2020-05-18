<template>
  <div class="main">
    <h1>{{title}}</h1>
    <p>{{date}}</p>
    <p>{{author}}</p>
    <p>
      动态语言是有用的工具。脚本使用户能够快速简洁地将复杂的系统连接在一起并表达想法，而不必担心诸如内存管理或构建系统之类的细节。
      近年来，像Rust和Go这样的编程语言使产生复杂的本地机器代码变得更加容易，这些项目是计算机基础架构中非常重要的发展。
      然而，我们声称拥有一个强大的脚本环境来解决广泛的问题领域仍然很重要
    </p>
    <p>
      JavaScript是使用最广泛的动态语言，可通过网络浏览器在每台设备上运行。大量的程序员精通JavaScript，并在优化其执行方面投入了大量精力。
      通过ECMA International之类的标准组织，对语言进行了认真，持续的改进。我们相信JavaScript是动态语言工具的自然选择； 无论是在浏览器环境中还是作为独立进程。
    </p>
    <p>
      我们在该领域的原始项目Node.js被证明是一个非常成功的软件平台。人们发现它对于构建Web开发工具，构建独立的Web服务器以及许多其他用例很有用。
      但是，Node是在2009年设计的，当时JavaScript是一种与众不同的语言。出于必要，Node必须发明一些概念，这些概念随后由标准组织采用，并以不同的方式添加到语言中。
      在演讲《Node的设计错误》中对此进行了更加详细的讨论。由于Node拥有大量用户，因此发展该系统既困难又缓慢。
    </p>
    <p>
      随着JavaScript语言的不断变化以及诸如TypeScript之类的新添加功能，构建Node项目可能会成为一项艰巨的工作，涉及管理构建系统和其他繁重的工具，这些工具摆脱了动态语言脚本的乐趣。
      此外，通过NPM存储库从根本上集中了链接到外部库的机制，这不符合Web的理想。
    </p>
    <p>
      我们认为JavaScript和周围的软件基础架构已经发生了足够的变化，值得进行简化。
      我们寻求一种有趣且高效的脚本环境，可用于多种任务。
    </p>
    <my-title text="一个用于命令行脚本的Web浏览器" href="#text1"></my-title>
    <p id="text1">Deno是一个新的运行时，用于在Web浏览器之外执行JavaScript和TypeScript。</p>
    <p>
      Deno试图提供一个独立的工具来快速编写复杂功能的脚本。 Deno是（并将始终是）单个可执行文件。 就像网络浏览器一样，它知道如何获取外部代码。 在Deno中，单个文件可以定义任意复杂的行为，而无需任何其他工具。
    </p>
    <pre class="pre-code">
    1  import { serve } from "https://deno.land/std@0.50.0/http/server.ts";
    2  
    3  for await (const req of serve({ port: 8000 })) {
    4    req.respond({ body: "Hello World\n" });
    5  }</pre>
    <p>
      在这里，通过一行代码将完整的HTTP服务器模块添加为依赖项。没有其他额外的配置文件，也不需要提前进行安装，只用执行<strong>deno run example.js</strong>。
    </p>
    <p>
      像浏览器一样，代码默认在一个安全沙箱中执行。未经允许，脚本无法访问硬盘驱动器，打开网络连接或进行任何其他潜在的恶意操作。
      浏览器提供了用于访问相机和麦克风的API，但用户必须首先授予权限。 Deno在终端中提供类似的行为。
      上述例子会执行失败，除非在命令行中提供标识 --allow-net。
    </p>
    <p>
      Deno小心不要偏离标准化的浏览器JavaScript API。 当然，并不是每个浏览器API都与Deno相关，但无论它们在哪里，Deno都不会偏离标准。
    </p>
    <my-title text="一流的TypeScript支持" href="#text2"></my-title>
    <p id="text2">
      我们希望Deno适用于广泛的问题领域：从小型单行脚本到复杂的服务器端业务逻辑。 随着程序变得越来越复杂，具有某种形式的类型检查变得越来越重要。 TypeScript是JavaScript语言的扩展，允许用户选择提供类型信息。
    </p>
    <p>
      Deno无需其他工具即可支持TypeScript。运行时在设计时考虑了TypeScript。deno types 命令为Deno提供的所有内容提供类型声明。Deno的标准模块全部使用TypeScript编写。
    </p>
    <my-title text="一流的TypeScript支持" href="#text3"></my-title>
    <p>
      Node是在JavaScript具有Promises或async/await概念之前设计的。
      Node中与promises相对应的是EventEmitter，它基于重要的API，即套接字和HTTP。
      除了async/await的人体工程学优势外，EventEmitter模式还存在背压问题。
      以TCP套接字为例。套接字在收到传入数据包时将发出“数据”事件。 这些“数据”回调将以不受限制的方式发出，从而使事件充满整个过程。
      由于Node继续接收新的数据事件，因此基础TCP套接字没有适当的背压，因此远程发送方不知道服务器已超负荷并继续发送数据。
      为了缓解此问题，添加了pause（）方法。这可以解决问题，但是需要额外的代码；
      而且由于泛洪问题仅在进程非常繁忙时才会出现，因此许多Node程序都可能被数据泛洪。
      结果是系统的尾部延迟时间很长。
    </p>
    <p>
      在Deno中，sockets仍然是异步的，但是接收新数据需要用户明确调用read()。
      正确构造接收套接字不需要额外的暂停语义。这不是TCP套接字独有的。
    </p>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import MyTitle from '@/components/Title.vue';

// 导航栏项目
interface NavItem {
  label: string,
  href?: string
}

@Component({
  components: {
    MyTitle
  }
})
export default class Header extends Vue {
  private title: string = 'Deno 1.0'
  private date: string = '2020--5-13'
  private author: string = 'Ryan Dahl, Bert Belder, and Bartek Iwańczuk'
  private navList!: NavItem[]

  private created() {
    this.navList = [
      { label: '安装', href: '' },
      { label: '手册', href: '' },
      { label: '标准库', href: '' },
      { label: '第三方模块', href: '' },
    ]
  }
}
</script>

<style lang="stylus">
.main {
  width: 80%;
  text-align: left;
  margin: 0 auto;
  max-width 768px
}
.pre-code
  border 1px solid rgb(210, 214, 220)
  border-radius .25rem
  padding .25rem .25rem
  background-color: rgb(246, 248, 250);
</style>
 