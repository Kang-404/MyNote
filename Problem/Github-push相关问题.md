# Github-push相关问题
在 ` push ` 该项目时，遇到一个错误：
```bash
Username for 'https://github.com': Kang-404
Password for 'https://Kang-404@github.com':
remote: Support for password authentication was removed on August 13, 2021.
remote: Please see https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently recommended modes of authentication.
fatal: Authentication failed for 'https://github.com/Kang-404/MyNote.git/'
```   

在网上找了很久都没有解决，后来在StackOverFlow上找到原因：
> If you enabled two-factor authentication in your GitHub account you won't be able to push via HTTPS using your accounts password. Instead you need to generate a personal access token. This can be done in the application settings of your GitHub account. Using this token as your password should allow you to push to your remote repository via HTTPS. Use your username as usual.

原来是从August 13, 2021之后就不支持通过https+密码向Github存取了。有两种解决方式：
- 第一种是修改项目remote方式为ssh方式，由于之前已经设置过ssh-key，所以修改之后可以直接push成功。
设置方式为：` git remote set-url origin git@github.com:OWNER/REPOSITORY.git `
详情可见：
[Managing remote repositories](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories)

- 第二种方式是 `Instead you need to generate a personal access token. `
详情可见：[Creating a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
