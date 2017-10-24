# Access model

cBackup user management is based on Yii2 RBAC model as implementation of [CSRC NIST RBAC](https://csrc.nist.gov/projects/role-based-access-control). Uou can read about Yii2 RBAC in [framework official documentation](http://www.yiiframework.com/doc-2.0/guide-security-authorization.html#rbac) or in [Yii2 cookbook](https://yii2-cookbook.readthedocs.io/security-rbac/#rbac). If you are used to Yii v1 RBAC model, make sure you update your knowledge, because Yii2 RBAC is different by obsoleting Role-Task-Permission chain and changing inheritance model.

!!! note
    At this moment RBAC model only limits access to API calls. Later it will be extended to handle access to different cBackup parts and functionality.

# User management

Alongside with regular users, there're three system users, that are considered as *'protected'*. These users can't be deleted or disabled, but you still are able to change passwords and access tokens for them:

* Username: `Java Core`; login: `JAVACORE`<br>
    is used as relation accessor between Java daemon and cBackup API<br><br>  
* Username: `Console APP`; login: `CONSOLE_APP`<br>
    is used for writing logs from console workers.<br><br>
* Username: `Admin`; login: `ADMIN`<br>
    is created during installation process and used as root access to cBackup. 

# Access rights

These entries represent RBAC model access-level entities of two types: Roles and Premissions. RBAC implements heirarchical access model. Role can have other role or permission as a heir. And permission can belong to a permission or to have other permission as a heir. Both entities can be standalone and not related to any other enity. There're also three *'protected'* entries:

* **admin**, type: `Role`<br>
    system entity for root user;<br><br>
* **APICore**, type: `Permission`<br>
    system entity for `Java Core` user granting him permission to invoke private API calls;<br><br> 
* **APIReader**, type: `Permission`<br>
    system entity granting permission to invoke public API calls.

# Rights assignment

These entries represent RBAC entities assignment to particular users. User can inherit both Roles and Permissions, granting access to certain permission with all related derivation tree (if exists).
