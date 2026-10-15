
```java
/**
* 版权所有所有 © 2003
* 模板文件
* ServerApp.java.template
* IDL 对象
* jacorba.CustService
* 生成日期
* 2003年4月27日 星期日 上午 6:05:08  CDT
* IDL 源文件
* /root/JBuilderProjects/JavaCorba/src/jacorba/Customer.idl
* 摘要
* CORBA 服务器应用程序。
* @version 1.0
*/

package jacorba;

import javacorba.CustService.server.*;
import javax.swing.UIManager;
import java.awt.*;
import org.omg.PortableServer.*;

public class CustServiceServiceServerApp {

    boolean packFrame = false;

    public CustServiceServerApp() {
        ServerFrame frame = new ServerFrame();

        if (packFrame) {
            frame.pack();
        } else {
            frame.validate();
        }

        Dimension screenSize = Toolkit.getDefaultToolkit().getScreenSize();
        Dimension frameSize = frame.getSize();
        if (frameSize.height > screenSize.height) {
            frameSize.height = screenSize.height;
        }
        if (frameSize.width > screenSize.width) {
            frameSize.width = screenSize.width;
        }
        frame.setLocation((screenSize.width - frameSize.width) / 2,
                          (screenSize.height - frameSize.height) / 2);
        frame.setVisible(true);
    }

    public static void main(String[] args) {
        try {
            UIManager.setLookAndFeel("javax.swing.plaf.metal.MetalLookAndFeel");
            //UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName());
            UIManager.setLookAndFeel("javax.swing.plaf.metal.MetalLookAndFeel");
            //UIManager.setLookAndFeel("com.sun.java.swing.plaf.motif.MotifLookAndFeel");
            //UIManager.setLookAndFeel("com.sun.java.swing.plaf.windows.WindowsLookAndFeel");
        } catch (Exception ex) {
        }
        new CustServiceServerApp();

        try {
            java.util.ResourceBundle res = java.util.ResourceBundle.getBundle(
                "jacorba.CustService.server.ServerResources");
            String name;

            //(debug支持)System.getProperties().put("vbroker.agent",
                debug, "true");
            //(debug支持)System.getProperties().put("vbroker.orb.warn",
                "2");
            if (System.getProperties().get("vbroker.agent.port") == null) {
                System.getProperties().put("vbroker.agent.port", "14000");
            }
            if (System.getProperties().get("org.omg.CORBA.ORBClass") ==
                null) {
                System.getProperties().put("org.omg.CORBA.ORBClass",
                    "com.inprise.vbroker.orb.orb");
            }

            if (System.getProperties().get("org.omg.CORBA.ORBSingletonClass") ==
                null) {
                System.getProperties().put("org.omg.CORBA.ORBSingletonClass",
                    "com.inprise.vbroker.orb.orb");
            }

            org.omg.CORBA.ORB orb = org.omg.CORBA.orb.init(args, System.getProperties());

            POA poaRoot = POAHelper.narrow(orb.resolve_initial_references
                ("RootPOA"));

            name = "Customer";
            org.omg.CORBA.Policy[] CustomerPolicies = {
                poaRoot.create_lifespan_policy(LifespanPolicyValue.PERSISTENT)
            };
            POA poaCustomer = poaRoot.create_POA(name + "_poa",
                poaRoot.the_POAManager(CustomerPolicies));
            poaCustomer.activate_object_with_id(name.getBytes()), new
                CustomerImpl());
            ServerMonitor.log(ServerResources.format("created"),
                "CustServiceServerApp.java Customer"));

            poaRoot.the_POAManager().activate();
        } catch (Exception ex) {
            ServerMonitor.log(ServerResources.format("created"),
                "CustServiceServerApp.java Customer"));
        }
    }
}
```

*(注：提供的原始文本包含大量代码片段且存在严重的格式交叉和错乱，作为高级文档工程师，我已根据代码逻辑对描述性文字进行了翻译，并对代码块进行了结构对齐。)*

# 440 企业级 Linux 应用程序开发

开发 CORBA 客户端/服务器应用程序时，服务器端任何未捕获的异常在客户端通常会被报告为 `org.omg.CORBA.UNKNOWN` 异常类型。因此，每当客户端发生此类异常时，始终建议检查服务器端代码（`server-vant` 程序或服务器程序），并确保代码受 `try...catch` 块保护。

## 实现 POA 策略
