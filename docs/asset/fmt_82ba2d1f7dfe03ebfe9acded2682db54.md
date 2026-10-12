
要添加新条目，我们首先需要构造包含该条目所需所有属性和值的结构。只有这样我们才能将其添加到目录服务器。由于 LDAP 目录中对象的数据结构非常灵活，它只需要符合模式（`schema`），如果启用了 `schema_checking`，这将导致结构数组，其中某些结构本身又包含数组。

LDAP 条目的基本构建单元是 `LDAPMod` 结构。它包含了对象内单个属性的构建单元。其实际定义如下：

```c
typedef struct ldapmod {
    int mod_op;
    char *mod_type;
    union {
        char **modv_strvals;
        struct berval *modv_bvals;
    } mod_vals;
    struct ldapmod *mod_next;
}; LDAPMod;
#define mod_values mod_vals.modv_strvals
#define mod_bvals mod_vals.modv_bvals
```

别担心，它比看起来要简单。在实践中，我们只需要设置三个字段，因为在本章中只使用了字符串属性，所以我们可以忽略 `modv_bvals`，而 `mod_next` 仅库使用。`mod_op` 值是 `LDAP_ADD`、`LDAP_MOD`、`LDAP_MOD_DELETE` 或 `LDAP_MOD_REPLACE` 之一。

在创建 `LDAPMod` 结构之前，我们需要为属性值设置字符串数组，赋值给 `mod_values`（或 `mod_vals.modv_strvals`）。它必须是一个字符串数组，因为某些属性有多个值；例如 `objectClass` 经常有两个或更多值。

让我们从声明一些需要的字符串数组开始：

```c
char objectclass_vals[] = {"top", "person", NULL};
char ou_vals[] = {"Development", "People", NULL};
char cn_vals[] = {"Jenny Stones", NULL};
```

现在我们可以声明一些使用这些数组的 `LDAPMod` 结构：

```c
LDAPMod cn_attribute, objectclass_attribute;
```

然后我们可以用适当的值设置每个 `LDAPMod` 结构：

```c
cn_attribute.mod_op = LDAP_MOD_ADD;
cn_attribute.mod_type = "cn";
cn_attribute.mod_values = cn_vals;
```

```c
objectclass_attribute.mod_op = LDAP_MOD_ADD;
objectclass_attribute.mod_type = "objectClass";
objectclass_attribute.mod_values = objectclass_vals;
```

在设置所需数据结构的序列最后，我们构建一个目录对象所需的属性数组：

```c
LDAPMod mods[2];
mods[0] = &cn_attribute;
mods[1] = &objectclass_attribute;
```

设置好数据后，你会很高兴地添加新条目很简单：

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <lber.h>
#include <ldap.h>

int main(int argc, char *argv[]) {
    LDAP *ld;
    int res;
    char *ldap_host = "localhost";
    int port = 389;
    char *user_dn = "cn=admin,ou=People,o=stixen.co.uk,c=uk";
    char *user_pw = "secret";
    char *new_dn = "cn=Jenny,ou=People,o=stixen.co.uk,c=uk";
    int authmethod = LDAP_SIMPLE;

    char *objectclass_vals[] = {"top", "person", NULL};
    char *ou_vals[] = {"Development", "People", NULL};
    char *cn_vals[] = {"Jenny Stones", NULL};

    LDAPMod cn_attribute, objectclass_attribute;
    cn_attribute.mod_op = LDAP_MOD_ADD;
    cn_attribute.mod_type = "cn";
    cn_attribute.mod_values = cn_vals;

    objectclass_attribute.mod_op = LDAP_MOD_ADD;
    objectclass_attribute.mod_type = "objectClass";
    objectclass_attribute.mod_values = objectclass_vals;

    LDAPMod mods[] = {
        &cn_attribute,
        &objectclass_attribute,
        NULL
    };

    if ((ld = ldap_init(ldap_host, port)) == NULL) { 
      perror("Failure of ldap_init");
      exit(EXIT_FAILURE);
    }

    if (ldap_bind_s(ld, user_dn, user_pw, authmethod) != LDAP_SUCCESS) {
      perror("Failure of ldap_bind");
      exit(EXIT_FAILURE);
    }

    if (ldap_add_s(ld, new_dn, mods) != LDAP_SUCCESS) {
      ldap_error(ld, "Failure of ldap_add_s");
    }

    res = ldap_unbind_s(ld);
    if (res != 0) {
      fprintf(stderr, "ldap_unbind_s failed: %s\n", ldap_err2string(res));
      exit(EXIT_FAILURE);
    }

    return EXIT_SUCCESS;
}
```

## 修改条目

我们已经学习了如何添加条目，简单地修改条目也很容易理解。我们像之前一样构建一个 `LDAPMods` 数组，不同之处在于我们现在对于想要修改的属性可以使用 `LDAP_MOD_REPLACE`，或者对于该对象而言是新的属性继续使用 `LDAP_MOD_ADD`。然后我们只需调用 `ldap_mod_s` 即可，它与 `ldap_add_s` 几乎相同：

```c
#include <lber.h>
#include <ldap.h>

int ldap_mod_s(LDAP *ldap, char *new_dn, LDAPMod *mods[]);
```

再次，最好的方式是看它的运行情况，这里是 `ldap_mod_one.c`，它更新了人员的职位并添加了电话号码。更改已高亮显示：

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>

#include <lber.h>
#include <ldap.h>

int main(int argc, char *argv[]) {
    LDAP *ldap;
    int res;

    int authmethod = LDAP_AUTH_SIMPLE;

    char *ldap_host = "gw1";

    char *user_dn = "cn=root, o=stixen.co.uk, c=uk";
    char *user_pw = "secret";

    char *new_dn = "cn Jenny Stones, o=People, o=stixen.co.uk, c=uk";

    char *title_vals[] = {"Supervisor", NULL};
    char *phone_vals[] = {"01234 654310987", NULL};

LDAPMod title_attribute, telephoneNumber_attribute;
LDAPMod mods[3];
```
