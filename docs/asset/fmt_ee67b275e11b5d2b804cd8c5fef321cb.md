
```java
import com.sun.rave.web.ui.component.TextArea;

import com.sun.rave.web.ui.component.Label;

import com.sun.rave.web.ui.component.Button;

import javax.faces.component.UIComponent;

import javax.faces.context.FacesContext;

import javax.faces.validator.ValidatorException;

import javax.faces.component.application.Message;

import javax.faces.component.html.HtmlPanel;

import javax.faces.validator.LengthValidator;

public class Validation extends AbstractPageBean {

    private int _placeholder;

    private void _init() throws Exception {

        nameLengthValidator.setMaximum(30);

    } // end method _init

// 为了节省空间，我们省略了第 36-345 行的代码。完整的
// 源代码在本章的示例中提供。

    public Validation() {
        // 空构造函数
    } // end constructor

    protected RequestBean getRequestBean() {
        return (RequestBean) getBean("RequestBean");
    } // end method getRequestBean

    protected ApplicationBean getApplicationBean() {
        return (ApplicationBean) getBean("ApplicationBean");
    } // end method getBean
```
| **Fig 26.19** | 用于验证用户输入并在有效时重新显示该输入的页面 bean。（第 1 部分，共 3 部分）。 |

## 第 26 章 Web应用程序：第一部分

```java
    protected SessionBean getSessionBean()
    {
        return (SessionBean) getBean("SessionBean");
    } // end method getSessionBean

    public void init()
    {
        super.init();
        try {
            _init();
        } // end try
        catch (ValidationInitializationFailure, e) {
            if (e instanceof FacesException) 
                throw new FacesException(e);
        } // end catch
    } // end method init

    public void preprocess()
    {
        // 空体
    } // end method preprocess

    public void prerender()
    {
        // 空体
    } // end method prerender

    public void destroy()
    {
        // 空体
    } // end method destroy

    public void emailTf_validate(FacesContext context, UIInputComponent component, Object value)
    {
        String email = String.valueOf(value);
        // 如果输入的邮箱地址不是有效格式
        if (!email.matches("\\w+([-.\\w]*)@\\w+([-.\\w]*)*\\.\\w+")) {
            throw new ValidatorException(new FacesMessage(
                "输入有效的邮箱地址，例如 user@domain.com"));
        } // end if
    } // end method emailTF_validate

    // 根据正则表达式对输入的邮箱地址进行验证，
    // 该正则表示有效邮箱地址的格式。
```

**Fig. 26.19** | 用于验证输入并在有效时重新显示输入的页面 bean。（第 2 部分，共 3 部分）。

```java
    public void phoneTF_validate( FacesContext context,
      UIComponent component, Object value )
    {
        String phone = String.valueOf( value );
        if // 如果输入的电话号码不是有效格式
          if (!phone.matches("(\\(\\d{3}\\)?(\\d{3}-)?\\d{4}))"))) {
            throw new ValidatorException(new FacesMessage(
              "输入有效的电话号码，例如 (555) 555-1234"));
        } // end if
    } // end method phoneTF_validate
```

// 在 Grid Panel 中显示表单项。
public String submitButton_action()
```java
{
    String name = String.valueOf(nameTF.getValue());
    String email = String.valueOf(emailTF.getValue());
    String phone = String.valueOf(phoneTF.getValue());
    nameResult.setValue(name);
    emailResult.setValue(email);
    phoneResult.setValue(phone);
    gridPanel.setRendered(true);
    return null;
} // end method submitButton_action
}// end class Validation
```
