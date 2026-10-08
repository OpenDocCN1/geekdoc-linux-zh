
超文本标记语言（HTML）用于标记网页使其能够在浏览器中渲染。曾在瑞士日内瓦核子研究中心（CERN）担任独立承包员的蒂姆·伯纳斯李（Tim Berners-Lee）于1989年提出了一种基于超文本并使用网络技术连接的交织文档系统。超文本是链接到其他文本文件的文本，由内瓦·布什（Vannevar Bush）于1945年提出，而道格拉斯·恩格尔伯特（Douglas Engelbert）于1968年演示了超文本的版本。伯纳斯李将这些概念结合并结合为标准通用标记语言（SGML）概述的基本方法，创建了一个可以独立创建文本文件，并通过超链接链接到其他文档的系统，从而产生了“冲浪”信息的需求，同时消除了对中心化管理分级文档结构的需求。HTML首次于1991年提出，互联网工程任务组（IETF）标准于1995年发布了2.0版本。HTML的最新版本是第5版，它包含了许多用于高度交互网站的特性。在考虑 HTML 的价值时，我们应该理解第一版本的 HTML 并没有在文档中引入图像的标准方法，即使在今天，它们与 HTML 标记页面也是分开的。HTML5 包含了对文档对象模型（DOM）良好设计且完整的支持，该模型将浏览器中呈现的文档分割若干独立的单元，以便于在浏览器沙箱内进行处理。结果是浏览器沙箱中的代码（例如 JavaScript）可以根据用户操作可靠地与页面元素进行交互。虽然这在早期版本中就可以设计，但当时没有建立的标准，开发者永远无法确定他们的代码是否会在所有浏览器上运行，甚至不知道浏览器更新是否会破坏代码并导致网站失效。HTML5 中标准化的另一个特性是拖放，即用户取屏幕上显示的对象并将其移动并释放到屏幕另一部分的能力。这一特性在支持触摸的界面中特别有用。

## 第十二章：移动电子商业开发

### 12.7.2 jQuery

JavaScript 用于编写可以在浏览器内执行的过程。它们支持能够进行丰富用户交互的动态网页。包含 JavaScript 的页面可以在用户的浏览器内完成业务数据处理步骤，清理并简化传输到应用程序服务器的数据传输。通过在网络浏览器上提供快速响应、高度交互的界面，用户体验得到了增强。由于数据传输仅在系列交互步骤后才进行，网络应用程序固有的延迟降低了。JavaScript 由 Netscape 在1995年首次引入，曾是 Netscape 浏览器的一项功能。它是一种脚本语言，与多平台编程语言 Java 几乎没有任何共同之处。JavaScript 代码在用户的浏览器中被解释，即按顺序翻译为代码。结果是，早期版本运行速度缓慢，除了在网页上添加一些交互特性（如下拉列表）之外，无法用于许多用途。随着时间的推移，JavaScript 的处理得到了改进，并开发了丰富的界面。这些界面在 Web 浏览器的 JavaScript 沙箱中运行。JavaScript 也用于 Web 服务端，使用服务器端编写简单的业务流程。

通过互联网访问网络应用程序，用户更倾向于提供丰富交互且没有网络数据传输延迟的应用程序。语言的增强，特别是 JavaScript 在浏览器上处理速度的提高，使得开发在用户设备上呈现高度交互界面的网络应用程序成为可能。JavaScript 编码在在高度动态电子商务环境中工作并开发不断调优系统的 Web 开发者中非常流行。虽然传统的程序员认为这种语言设计不当且不可靠，但这种语言成为了为网站提供交互性的主要手段。在行业中，使用脚本模块来自动化常用功能已成为常态。一个例子是 jQuery 库，它最初提供块可重用代码来为网页添加特殊特效。最初的使用限于网页增强，JavaScript 也因其安全漏洞而受到一些批评，特别是因为某些漏洞可以使其被用于跳出浏览器沙箱并感染宿主机。

随着异步 JavaScript 和 XML（AJAX）的流行，它重新回回了重要地位，网页的片段可以在用户的浏览器中进行本地处理。AJAX 创建了诸如 Google Maps 应用这样的网络应用程序的丰富界面。新的库被开发出来，通过添加预包代码模块为网站添加额外功能。

### 12.7.3 JavaScript 模块

jQuery 是一个流行的用于文档导航和事件处理的 JavaScript 库。其中一个特性——遍历（traversal），使得编写遍历页面中元素的代码变得简单。该特性的用途之一是遍历表单中的所有字段，并确保字段输入的数据符合标准。由于代码在浏览器上运行，测试在输入数据时执行，没有延迟或流量，且仅将清洁的数据发送到业务服务器。另一个特性——操作（manipulation），允许代码替换或更改页面不同元素中的数据。jQuery 架构还支持为新功能开发插件，这些插件可以轻松地添加到网站中。有一个庞大的 jQuery 插件库，这使得开发具有丰富元素（如交互式日历、计算器或图像库）的网站变得非常容易。通过编写一次并重复使用代码，提高了编码生产力和可靠性，并降低了控制维护成本。在 jQuery 中，这种方法比编写代码更容易，即使用预构建组件并将它们补凑成网站，而不是直接编写代码。这种方法使用了经过测试的代码模块，不仅缩短了代码开发时间，而且证明比自编写的代码更可靠。一项比较移动课堂互动有效性的有趣研究显示，移动应用带来了显著改进，顺便提到该应用是使用 jQuery 框架构建的（Kert, 2013）。

### 12.7.4 课程

MIT App Inventor 是一个基于 Web 的平台，提供拖放界面来设计移动设备应用程序。它旨在向正在学习第一门编程课程的学生（尤其是高中生）教授应用开发的基础。界面有限，但易于学习。斯坦福 iPhone 开发课程是一门完整的 iPhone 应用编程本科课程（CS193P），使用 Objective C（一种用于 Mac OS/X 和 iOS 开发的语言），专注于为 iPhone 开发移动应用程序。这是一门高强度课程，要求预先具备过程化编程语言的计算机编程知识。斯坦福几门先修课程也通过 iTunes University 提供。该课程自 2009 年冬季以来以学期形式在线提供。虽然该课程为斯坦福学生提供积分，但讲座已发布在 iTunes University 上供公众访问。另一门课程认可了移动应用使用的多学科性质，侧重于聚集来自不同背景的学生来构建移动应用（Massey et al., 2006）。

第十二章：移动电子商务开发 235

## 12.8 总结

开发移动电子商务应用程序在许多方面与其它应用程序相似。电子商务应用程序倾向于拥有许多云端组件，并依赖于与其他企业的有效交互。移动应用需要考虑位置、交互和界面的使用语境差异。根据原则，由于移动应用的生命周期短，且需要满足快速变化的喜好，移动应用通常使用快速应用开发技术，利用预构建的插件模块和云服务来构建。移动电子商务开发者面临的另一个挑战是需要使用自定义程序来增强不同类型硬件上的应用性能。

移动应用开发者可以选择构建一种基于 Web 的应用程序，并针对移动设备、屏幕尺寸和触摸输入进行定制。由于许多笔记本电脑正在被使用，大平板电脑网页浏览正变得流行，生成的 Web 应用可以实现真正的跨平台。另一种方法是构建原生应用，利用特定的硬件功能并获得高度交互的性能。这种方法对于游戏、沉浸式应用以及经济效益合理的业务应用程序是必需的。在许多电子商务场景中，可以使用混合方法，即开发 Web 应用，并结合较小的原生应用来丰富部分模型，使用自定义功能来改进交互。

## 参考文献

ABI Research. (2013). 企业与移动应用——如何做到正确，2013 年 10 月 15 日，https://www.abiresearch.com/webinars/enterprises-and-mobile-apps-how-get-it/

Abrahamson, P., Hanhineva, A., Hutko, H., Ihne, T., Jäälino, J., Korkala, M., Koskela, J., Kyönen, P., and Palo, O. (2004). Mobile-D: 一种移动应用开发的敏捷方法。ACM 19th Annual ACM Conference on Object-Oriented Programming, Languages, and Applications (OOPSLA), Vancouver, British Columbia, Canada, 2004.

Barthold, C., Kubbu, K.P., and Dantu, R. (2011). 嵌入陀螺仪的手机评估。2011 IEEE International Conference on Systems, Man. and Computing (ICSMC), Anchorage, AC, 2011 年 10 月 9–12 日，p. 1632–1638. doi: 10.1109/ICSMC.2011.6083905.

Christophe, B., Narganes, M., Antila, V., and Maknicius, L. (2011). 非间歇性内容分发的移动执行。Bell Labs Journal, 15(4), 117–134.

Cimino, M.A. and Marcelloni, F. (2012). 一种开发设备无关移动应用的高效模型方法。Journal of Architecture, 58(8), 286–304. doi:10.1016/j.jsysarc.2012.06.001.

## 移动电子商务

Crosman, P. (2013). 移动银行响应式设计的争论。American Banker, 178(318), 18.

Dalmaso, I., Datta, S.K., Bonnet, C., and Nikaein, N. (2013). 跨平台移动应用开发工具的调查、比较与评估。第九届国际无线通信与移动计算会议 (IWCMC), Sardinia, Italy, 2013 年 7 月 1-5 日，pp. 323–328. doi: 10.1109/IWCMC.2013.6583580.

Denis, J. and Peter, G. (2012). 五十 fantastic响应式设计工具，Creative Bloq。2012 年 4 月 24 日，http://www.creativebloq.com/css/responsive-web-5132270.

Everhardt, C. (2012). 使用 apache cordova 开发 HTML5 Windows 应用。MDS, 27(5), 28–42.

Fisher, M. and Bauer, D. E. (2006). 构建移动学习：利用技术实现高等教育中的主动教育、探索、协作、评估和反思。Journal of Educational Technology Systems, 35(1), 3–30.

Floyd, D. (2006). 移动应用系统规模 (MASS)。Bell Labs Technical Journal, 21(3), 191–198.

Frederick, K. S. (2013). 响应式 Web 设计 101。Computers in Libraries, 33(6), 11–24.

Greene, K. (2009). 交互的性。Review Technology, 112(5), 112–114.

Haghihi, P., Krishnaswamy, S., Zaslavsky, A., Gaber, M., Sinha, A., and Gillick, B. (2013). Open mobile miner：用于构建情境感知数据挖掘的工具包。Journal of Organizational Computing & Electronic Commerce, 23(3), 224–248. doi:10.1080/10939522013.80713

nisomuru, P., Finnman, R., Isomuru, M., and Spasevic, M. (2008). 移动互联网的方法。Knowledge, Technology & Policy, 24(4), 259–268.

Kert, S. (2013). 使用移动技术支持教学课程。Journal of Educational Research, 48(4), 431–445. doi:10.2190/ECR.48.4.

Keynote.(2013a). 移动应用的策略与策略，白皮书。2013 年 10 月 15 日，http://www.keynote.com/whitepapers/WP_Strategies.

Keynote.(2013b). 2013 年 11 月 1 日，http://keynote.com/support/usecases.

Liszewski, A. (2013). 触摸让触摸屏功能。Gizmo。http://gizmo.com/44125694/design-lets-you-features-on-touchscreen-by-tapping.

Marotte, E. (2011). 。

Massey, A., Ramesh, R., and Khatri, V. (2006). 移动应用的设计、开发与评估：基于问题的学习。IEEE Transactions on Education, 49(2), 183–192. doi:10.1109/TE.2006.87500.

Matsakura, K. (2013). 让移动 Web 快起来。Communications of ACM, 57(6), 56–61. doi:10.1145/242856.242857.

Mucci, H., Di Francesco, A., and Esposito, P. (2012). 移动应用软件测试：挑战与方向。第七届软件测试研讨会 (AST), Zurich, Switzerland, 2012 年 6 月 2–3 日，pp. 29–35. doi:10.1109/IWAST.2012.622887.

Nicolaou, A. (2013). 。Communications of ACM, 56(8), 45–51. doi:10.1145/249207.249203.

第十二章：Flood, D., 移动电子商务

Nosseir, A., Flood, R., Ibrahim, O. (2012). 移动开发。第七届计算机工程与系统会议 (ICCES), Cairo, Egypt, 2012 年 11 月 27–29 日，pp. 281–286.

Oulsavirta, A., Tamminen, S., Roto, V., and Kuorelahhti, J. (2005). 4秒爆发交互：移动 HCI 中注意力资源的碎片化。Proceedings of the SIGCHI on Human Factors in Computing Systems, Portland, OR, 2005 年 4 月，pp. 919–928.

Palmersi, M., Singh, I., and Cchetti, A. (2012). 跨平台移动开发工具。下一代网络智能会议 (ICIN), Berlin, Germany 2012 年 8–11 日，pp. 179–186. doi: 10.1109/ICIN.2012.637023.

Rin, H. and Hahn, J. (2011). 移动无障碍性、挑战与最佳实践。第14届 Accessibility Higher Ground Media, Web and Technology Conference, Boulder, CO, 2011 年 11 月 14–18 日。

Ruiz, J., Li, Y., and Link, E. (2021). 移动交互的用户自定义手势。CHI Proceedings, Vancouver, Canada, 2021 年 5 月 7–11 日，pp. 197–206.

Serm, T., Blanchfield, P., and Su, K.S. (2006). 移动报开发框架：部署移动网站创建指南。ICOOC '06 国际计算与信息会议，Kuala Lumpur, Malaysia, 2006 年 6 月 6–8 日，pp. 1–8. doi: 10.1109/ICOOC2006.527643.

Shiraz, M., Abfolazli, S., Saneei, Z., and Gani, A. (2013). 移动云计算中应用外包的移动交互研究。Journal of Supercomputing, 63(3), 946–964. doi: 10.1007/s11227-012-0846-y.

Steele, B. (2003). 绘制出来，http://www.gadget.com/2003/08/26/wacom-intuos-creative-stylus-hands-on/。访问于2013 年 10 月 15 日。

Tarasewich, P. (2003). 设计移动电子商务应用。Communications of ACM, 46(12), 57–60.

Unhelkar, B. and Murugesan, S. (2010年5-6月)。企业级移动应用开发框架。IT Professional, 12(3), 33–39. doi: 10.1109/TIP.2010.45

Vervelen, T., Simoens, P., De Turck, F., and Dhoedt, B. (2012). AIOLOS：通过网络觅寻提升移动应用性能的移动应用开发框架。Journal of Systems, 85(11), 2629–2639. doi:10.1016/j.jss.2012.06.011.

Wacom. (2013). HTML语音器小组最终报告，2011 年 12 月 6 日，http://www.wacom.com/2005/Incubator/htmlpeech/XGRhtmlpeech-201106/

Zhu, W., Liu, L., Yin, S., Hu, H., Tang, E., and Wei, S. (2013). 基于运动传感器融合的手势识别及其用于移动设备的 VLSI 架构。International Journal of Electronics, 101(5), 621–635. 10.1080/00207217.2013.794822.

# 移动电子商务应用与移动业务

# 第十三章
