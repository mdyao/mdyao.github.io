
### install texlive
```
sudo apt-get install texlive
```

### install sublime-text
```
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
sudo apt-get install apt-transport-https
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt-get update
sudo apt-get install sublime-text

%% apt-get install latexmk
```

### install Package-control
```
import urllib.request,os,hashlib; 
h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; 
pf = 'Package Control.sublime-package'; 
ipp = sublime.installed_packages_path(); 
urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) );
by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); 
dh = hashlib.sha256(by).hexdigest(); 
print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by) 

```

### install dbus
```
cd ~/下载
tar xzvf dbus-python-1.2.4.tar.gz
sudo apt-get install libdbus-glib-1-dev
cd dbus-python-1.2.4
./configure
make
sudo make install
```

### Ubuntu安装Sublime Text 3--解决无法使用搜狗中文输入法
http://www.qingzz.cn/ubuntu_sublime_sogou



