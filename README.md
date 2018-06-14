# kubeconfig-generator
Kubeconfig Generator

Prerequisite
------------

gettext
Install with brew:

brew install gettext
Installs the libraries and the utilities:

autopoint envsubst gettext gettext.sh gettextize msgattrib msgcat msgcmp msgcomm msgconv msgen msgexec msgfilter msgfmt msggrep msginit msgmerge msgunfmt msguniq ngettext recode-sr-latin xgettext
But doesn’t add to your path! You need to modify the env. variable $PATH:

vi ~/.bash_profile
And add to the end or modify previous declarations:

export PATH=${PATH}:/usr/local/opt/gettext/bin
