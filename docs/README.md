Agency Jekyll theme
====================

Agency theme based on [Agency bootstrap theme ](https://startbootstrap.com/template-overviews/agency/)

# About

Images are in '/img/about/'

# Team

Team members and info are in '_config.yml'

Images are in '/img/team/'


# Development

    jekyll serve --livereload

# Deployment

    #!/bin/sh
    # rebuild
    rm -rf _site
    jekyll build

    echo 'Compressing...'
    tar -czvf archive.tar.gz ./_site --exclude=./_site/deploy* >/dev/null 2>&1
    # tar -czvf node.tar.gz --exclude=features/node_modules features >/dev/null 2>&1
    echo 'Compressed archive.tar.gz'

    echo 'Start transfer compressed file to ali cloud...'
    scp -r archive.tar.gz tenty-web:~

    echo 'Unpack tar file in the remote server...'
    unzip_command="tar -xzvf archive.tar.gz -C /srv/www --transform 's/_site/tenty.co/' >/dev/null 2>&1;\
    rm archive.tar.gz;\
    exit"
    ssh tenty-web  "$unzip_command"
    rm archive.tar.gz

    echo 'Done'


