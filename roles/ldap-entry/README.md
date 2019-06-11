**用途：** 新增與刪除 ldap 帳戶，可一次新增與刪除多個 ldap 帳號

**預設值：**
>使用此 ansible role 建立的 ldap 帳戶，預設密碼為 ***password***

**操作步驟：** 

1. git clone 本專案到本地電腦
2. **新增 ldap 帳戶**，修改 defaults/main.yml 變數檔案，填入以下資料：

   **----- defaults/mail.yml -----**

   ...(省略)

   **`-`cn:** jackylee  (輸入完整英文名姓，不要有 '.' 或 '-' 等符號)

   **gn:** jacky   (輸入英文名)

   **sn:** lee   (輸入英文姓)

   **email:** jackylee@hotmail.com  (輸入電子郵件)

   **uidnum:** "{{ uidnumber.``0`` }}"  (如果只新增一個帳號，輸入 uidnumber.``0``, 如果要新增多個，第二個為 uidnumber.``1``, 第三個為 uidnumber.``2``...依此類推)

   **pwd:** (預設為 **``password``** 並且用 MD5 編碼，**``請不要修改``**)

   **`-`cn:** peterwang (第二個帳號，如上面格式輸入即可)

   ...(省略)

  3. 存檔離開。

  4. 執行 ansible-playbook 指令，請注意 inventory 指定只能是 **``本機 (locahost 或者 127.0.0.1)``**，指令如下：

> **ansible-playbook ldap-entry -e ``job=add`` -vvv**   (引用變數 ``job=add`` 表示執行新增 ldap 帳戶 tasks)

  5. **刪除 ldap 帳戶**，修改 defaults/main.yml 變數檔案，填入以下資料：

  **----- defaults/mail.yml -----**

  ...(省略)

  absent_users:

    - jackylee (輸入完整英文名姓，不要有 '.' 或 '-' 等符號)

    - peterwang  (輸入完整英文名姓，不要有 '.' 或 '-' 等符號)

  6. 存檔離開。
  
  7. 執行 ansible-playbook 指令，請注意 inventory 指定只能是 **``本機 (locahost 或者 127.0.0.1)``**，指令如下：

  > **ansible-playbook ldap-entry -e ``job=absent`` -vvv**   (引用變數 ``job=absent`` 表示執行刪除 ldap 帳戶 tasks)
