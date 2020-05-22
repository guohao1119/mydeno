<template>
  <div class="main">
    <div class="div-img">
      <img :src="deno" alt="deno">
    </div>
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
    <my-title text="Promise一直往下" href="#text3"></my-title>
    <p id="text3">
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
      系统的最低级别绑定层从根本上与promises相关联，我们称这种绑定为"ops"。
      Deno中所有形式的回调都来自promises。
    </p>
    <p>
      Rust有其自己的类似于promise的抽象，称为Futures。 通过"op"抽象，在Deno中将Rust的基于future的API绑定到JavaScript promise中变得容易。
    </p>
    <my-title text="Rust API" href="#text4"></my-title>
    <p id="text4">
      我们提供的主要组件是Deno命令行界面（CLI）。CLI是今天的1.0版本。
      但是Deno并不是一个整体的程序，而是设计为Rust板条箱的集合，以允许在不同的层进行集成。
    </p>
    <p>
      deno_core箱子是Deno的裸露骨头版本。
      它不依赖于TypeScript或Tokio。
      它只是提供了我们的运营和资源基础架构。
      也就是说，它提供了一种将Rust期货绑定到JavaScript promise的有组织方式。
      CLI当然完全建立在deno_core之上。
    </p>
    <p>
      rusty_v8条板箱可为V8的C++ API提供高质量的Rust绑定。
      该API尝试尽可能与原始C++ API匹配。
      这是零成本的绑定-Rust中公开的对象与您在C++中操作的对象完全相同。
      （例如，先前对Rust V8绑定的尝试强制使用了持久句柄。）
      板条箱提供了在Github Actions CI中内置的二进制文件，但它还允许用户从头开始编译V8并调整其许多构建配置。
      所有V8源代码均在包装箱中分发。最后，rusty_v8尝试成为一个安全的接口。
      它还不是100％安全的，但我们正在接近。
      能够以安全的方式与像V8这样复杂的VM进行交互非常令人惊讶，并且使我们能够发现Deno本身中的许多困难错误。
    </p>
    <my-title text="稳定性" href="#text5"></my-title>
    <p id="text5">
      我们保证在Deno中保持稳定的API。
      Deno有很多接口和组件，因此透明地了解我们所说的“稳定”是很重要的。
      我们发明的与操作系统交互的JavaScript API都可以在“Deno”命名空间（例如Deno.open（））中找到。
      这些已经过仔细检查，我们不会对它们进行向后不兼容的更改。
    </p>
    <p>
      尚未准备稳定的所有功能都隐藏在--unstable命令行标志后面。
      您可以在此处查看不稳定接口的文档。在后续版本中，其中一些API也将被稳定。
    </p>
    <p>
      在全局名称空间中，您会找到各种其他对象（例如setTimeout（）和fetch（））。
      我们已经尽力使这些界面与浏览器中的界面相同。
      但是如果发现意外的不兼容性，我们将发出更正。
      浏览器标准定义了这些接口，而不是我们。
      我们发布的所有更正均是错误修复，而不是界面更改。
      如果与浏览器标准API不兼容，则可以在主要版本之前更正该不兼容。
    </p>
    <p>
      Deno也有许多Rust API，即deno_core和rusty_v8条板箱。
      这些API都不是1.0。
      我们将继续对它们进行迭代。
    </p>
    <my-title text="局限性" href="#text6"></my-title>
    <p id="text6">
      重要的是要了解Deno不是Node的分支-它是一个全新的实现。
      Deno的开发仅两年时间，而Node的开发已超过十年。
      考虑到对Deno的兴趣，我们希望它会继续发展和成熟。
    </p>
    <p>
      对于某些应用程序而言，Deno可能是当今的不错选择，对于其他应用程序而言则尚未。
      这将取决于要求。我们希望对这些限制保持透明，以帮助人们在考虑使用Deno时做出明智的决定。
    </p>
    <my-title text="兼容性" href="#text7"></my-title>
    <p id="text7">
      不幸的是，许多用户会发现与现有JavaScript工具的兼容性令人沮丧地缺乏。
      通常，Deno与Node（NPM）软件包不兼容。
      在 https://deno.land/std/node/ 上建立了一个新生的兼容性层，但还远未完成。
    </p>
    <p>
      尽管Deno采用强硬方法简化了模块系统，但最终Deno和Node是目标相似的非常相似的系统。
      随着时间的推移，我们希望Deno能够开箱即用地运行越来越多的Node程序。
    </p>
    <my-title text="HTTP服务器性能" href="#text8"></my-title>
    <p id="text8">
      我们不断跟踪Deno的HTTP服务器的性能。
      问候世界的Deno HTTP服务器每秒处理约25,000个请求，最大延迟为1.3毫秒。
      一个可比的Node程序每秒处理34,000个请求，最大延迟介于2到300毫秒之间。
    </p>
    <p>
      Deno的HTTP服务器是在本机TCP套接字顶部的TypeScript中实现的。
      Node的HTTP服务器使用C语言编写，并作为对JavaScript的高级绑定公开。
      我们一直拒绝将本地HTTP服务器绑定添加到Deno的冲动，因为我们要优化TCP套接字层，更常见的是优化op接口。
    </p>
    <p>
      Deno是一个合适的异步服务器，每秒25k请求足以满足大多数目的。
      （如果不是，那么JavaScript可能不是最佳选择。）
      此外，由于普遍使用Promise（如上所述），我们期望Deno通常表现出更好的尾部延迟。
      综上所述，我们确实相信该系统还有更多的性能优势，我们希望在将来的版本中实现这一目标。
    </p>
    <my-title text="TS编译器瓶颈" href="#text9"></my-title>
    <p id="text9">
      在内部，Deno使用Microsoft的TypeScript编译器检查类型并生成JavaScript。
      与V8解析JavaScript所花费的时间相比，它非常慢。
      在项目的早期，我们曾希望“ V8快照”在此能够带来重大改进。
      快照肯定有帮助，但是它仍然缓慢地令人满意。
      我们当然认为可以在现有TypeScript编译器的基础上进行一些改进，但是对我们来说很显然，最终需要在Rust中实现类型检查。
      这将是一项艰巨的任务，不会很快发生。 但它可以在开发人员经历的关键路径上提供数量级的性能改进。
      TSC必须移植到Rust。如果您有兴趣合作解决此问题，请与我们联系。
    </p>
    <my-title text="插件/扩展" href="#text10"></my-title>
    <p id="text10">
      我们有一个新生的插件系统，用于通过自定义操作扩展Deno运行时。
      但是，此接口仍在开发中，并已标记为不稳定。因此，访问Deno提供的系统以外的本机系统很困难。
    </p>
    <my-title text="致谢" href="#text11"></my-title>
    <p id="text11">
      致谢。。。
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
  private deno: object = require('@/assets/images/deno.jpg')
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

<style lang="stylus" scoped>
.main {
  width: 80%;
  text-align: left;
  margin: 0 auto;
  max-width 768px
}
.div-img
  width 100%
  background-color rgb(47, 46, 44)
  img
    width 100%
    max-width 1024px
.pre-code
  border 1px solid rgb(210, 214, 220)
  border-radius .25rem
  padding .25rem .25rem
  background-color: rgb(246, 248, 250);
</style>
 