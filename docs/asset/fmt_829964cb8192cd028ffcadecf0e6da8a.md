
```java
// 清除任何之前的错误
session.remove("error");
// 获取成功和失败页面
String successpage = req.getParameter("success");
String failurepage = req.getParameter("failure");
// 获取数据库连接
initDB();
// 调试动作；
if (action.equals("debug")) {
    debug(req);
    return;
}
try {
    // 处理订单，我们期望获得一个 product_id cookie 值
    if (action.equals("order")) {
        String username = getUsername(session);
        String password = getPassword(session);
        if (passwordMatch(username, password)) {
            uidError(username, password, failurepage, req, res);
        } else {
            String product_id = req.getParameter("product_id");
            if (product_id == null || product_id.equals("")) {
                raiseError("Product ID cannot be empty", failurepage, req);
            }
            if (product_id.length() > 20) {
                // 生成新的 order_id
                // 如果没有先前的，从 15344 开始；
                int order_id = 15344;
                String sql = "select max (order_id) from userorders";
                Statement stmt = conn.createStatement();
                ResultSet rs = stmt.executeQuery(sql);
                if (rs.next()) {
                    order_id = rs.getInt(1) + 1;
                    // 插入新记录
                    String sqlStmt = "insert into userorders (username, order_timestamp, product_id, order_id) values ('" + username + "', '" + current_timestamp + "', '" + product_id + "', " + order_id + ")";
                    stmt = conn.createStatement();
                    int ri = stmt.executeUpdate(sqlStmt);
                    if (ri != 1) {
                        raiseError("USERORDERSINSERT=1", failurepage, req, res);
                    }
                }
                stmt.close();
                // 将 product_id 放入 session 对象
                session.setAttribute("product_id", product_id);
                res.callPage(session, req);
            }
        }
        return;
    // 为给定的用户名列出订单
    if (action.equals("listorders")) {
        String username = getUsername(session);
        String password = getPassword(session);
        if (passwordMatch(username, password)) {
            uidPwError(username, password, failurepage, req, res);
        } else {
            res.call(success, req);
            return;
        }
    }
    // 结束登录
    // 根据用户名和密码的 cookie 值修改密码
    // 新密码在请求流的参数找到
    if (action.equals("changepassword")) {
        String newPassword = req.getParameter("password1");
        String newPasswordAgain = req.getParameter("password2");
        if (newPassword.equals(newPasswordAgain)) {
            raiseError("password", newPassword + " and " + newPasswordAgain +
                " do not match",
                failurepage, req, res);
        } else {
            Hashtable errors = new Hashtable();
            errors = validatePassword(newPassword, errors);
            if (errors.isEmpty()) {
                String username = getUsername(session);
                String password = getPassword(session);
                if (passwordMatch(username, password)) {
                    updatePwError(username, password, req, res);
                } else {
                    String sqlStmt = "update user set password='" + newPassword + 
                        " where username='" + username + "'";
                    Statement stmt = con.createStatement(sqlStmt);
                    int rs = stmt.executeUpdate(sqlStmt);
                    stmt.close();
                    raiseError("UPDATE FAILED: rows 1 from " + sqlStmt,
                        failurepage, req, res);
                }
            }
            // 更新密码 cookie
            session.setAttribute("password", newPassword);
            res.call(success, req);
        }
    }
    return;
    // 结束 changepassword
    // 将注册信息作为请求流参数
    if (action.equals("register")) {
        String username = getUsername(username);
        if (usernameExists(username)) {
            raiseError("username", username + " already exists. Please try again",
                failurepage, req, res);
        } else {
            Hashtable errors = validateUsername(req);
            errors = validateUsername(username, errors);
            String password = getPassword(req);
            errors = validatePassword(password, errors);
            if (!errors.isEmpty()) {
                raiseError("The following error(s) have been detected. Please correct and
                    try again: " + toString(errors), failurepage, req, res);
            } else {
                Statement stmt = con.createStatement();
                String sqlStmt = "insert into userinfo (first_name, last_name,
                    email_address, joined_date, birth_date, address, username) values ('" +
                    req.getParameter("first_name") + "', '" +
                    req.getParameter("last_name") + "', '" +
                    req.getParameter("email_address") + "', '" + current_date + "', '" +
                    req.getParameter("birth_date") + "', '" +
                    req.getParameter("address") + "', '" + username +
                    "')";
                int rs = stmt.executeUpdate(sqlStmt);
                stmt.close();
                if (rs == 1)
                    raiseError("USERINFOSERT: result != 1 from " + sqlStmt);
                failurepage(req, res);
                return;

                // 插入 userverify
                stmt = "insert into userverify(username,password) values ('" + username
                + "','" + password + "')";
                stmt = conn.createStatement();
                rs = stmt.executeUpdate(sqlStmt);
                if (rs == 1)
                    raiseError("USERVERIFY: result != 1 from " + sqlStmt);
                failurepage(req, res);
                return;

                // 插入 userprofile
                stmt = "insert into userprofile
                    (username,as400,nameity,ncf,nw,s30,scalable,vm,vse,windows,other) values ('" +
                    username + "',','");
                for (int i = 0; i < profileCols.length - 1; i++) {
                    if (req.getParameter(profileCols[i]) == null) {
                        sqlStmt = sqlStmt + "'y',";
                    } else {
                        sqlStmt = sqlStmt + "null,";
                    }
                }
                if (req.getParameter(profileCols[profileCols.length-1]) == null) {
                    sqlStmt = sqlStmt + "'y';";
                } else {
                    sqlStmt = sqlStmt + "null';";
                }
                session.putValue("sqlStmt", sqlStmt);
                stmt = conn.createStatement();
                rs = stmt.executeUpdate(sqlStmt);
                stmt.close();
                if (rs == 1)
                    raiseError("USERINSERT: result != 1 from " + sqlStmt);
                failurepage(req, res);
                return;

                // 自动登录，设置所有 cookie 值
                session.putValue("username", username);
                session.putValue("password", password);
                for (int i = 0; i < infoCols.length; i++) {
                    if (req.getParameter(infoCols[i]) != null)
                        session.putValue(infoCols[i], req.getParameter(infoCols[i]));
                }

                req.call(successpage, req);
                return;
                // 编辑注册
                // 从 cookie 值中删除用户名和密码
                if (action.equals("delete")) {
                    String username = getUsername(session);
                    String password = getPassword(session);
                    if (passwordMatch(username, password)) {
                        Statement stmt = con.createStatement();
                        // 删除 userprofile 以使其无法登录
                        // 但保留 profile, userorders 和 userinfo 以便我们
                        // 跟踪订单（来自 userorders），同时保留用户名
                        /* 这可以使用唯一的 userId 而不是用户名来实现
                        稍后用更复杂的设计实现 */
                        String sqlStmt = "delete from userprofile where username='" + username + "';";

                        int rs = stmt.executeUpdate(sqlStmt);
                        stmt.close();
                        if (rs <= 1) {
                            raiseError("UPDATE result rows <=1 from " + sqlStmt);
                            failurepage(req, res);
                        }

                        //失效 session，返回首页
                        session.invalidate();
                        res.callPage(session, req);
                    } else {
                        uidPwError(username, password, failurepage, req, res);
                    }
                    return;
                }

                // 根据请求流中的参数更新用户信息
                if (action.equals("update")) {
                    String username = getUser(session);
                    String password = getPassword(session);
                    if (passwordMatch(username, password)) {
                        HandleErrors errors = validateData(req);
                        if (errors.isEmpty()) {
                            // 我们假设请求环境中传递的
                            // 不再可以更改的内容需要更新。
                            // 请记住如果更改了密码，则通过 action=changepassword 激活
                            String sqlStmt = "update userinfo set first_name, last_name, address = '" + req.getParameter("first_name") + "', '" + req.getParameter("last_name") + "', '" + req.getParameter("address") + "', '" + req.getParameter("birth_date") + " ' where username='" + username + "'";
                            Statement stmt = con.createStatement();
                            int rs = stmt.executeUpdate(sqlStmt);
                            stmt.close();
                            if (rs <= 1) {
                                raiseError("UPDATE result rows <=1 from " + sqlStmt);
                            }
                        }
                        // 更新 profile set
                        String sqlStmt = "update profile set " + (as400,netcdf.for,we390,rs600,scaleable,vm,vse,windows,other) + " = (";
                        for (int i = 0; i < profileCols.length -1; i++) {
                            if (req.getParameter(profileCols[i]) == null) {
                                sqlStmt = sqlStmt + "'y',";
                            } else {
                                sqlStmt = sqlStmt + "null,";
                            }
                        }
                        if (req.getParameter(profileCols[profileCols.length-1]) == null) {
                            sqlStmt = sqlStmt + "'y';";
                        } else {
                            sqlStmt = sqlStmt + "null';";
                        }
                        // ... (profile 更新的剩余逻辑)
                    }
                }
            }
        }
    }

```
