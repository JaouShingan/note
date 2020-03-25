# Git

## git push 免密码

1.在用户目录下执行以下代码

    touch .git-credentials
    vim .git-credentials
    https://{username}:{password}@github.com
    http://{username}:{password}@github.com

2.设置config

执行代码

    git config --global credential.helper store

完成。