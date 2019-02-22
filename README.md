Bu dokuman Vagrant ve Ansible ile LA demo ortami kurulumunu anlatmaktadir. Tum Lider-Ahenk bilesenleri ayri birer Virtualbox sanal makinasi olarak olusturulacaktir. Kurulan sistem gelistirme sirasinda test amacli veya demo ortami olarak da kullanilabilir.

## Kurulum Gereksinimleri
Kurulum icin kullanilacak olan fiziksel makinada (guncel bir linux versiyonu tavsiye edilir) git, vagrant (2.1.2) ve ansible (2.7.0) kurulu olmalidir. Bu uygulamalarin daha yeni versiyonlarinin kurulmasi durumunda sorun cikmasi beklenmemektedir ancak testleri yukarida belirtilen versiyonlar ile yapilmistir.


#### Internet Erisimi
LA bilesenlerinin kurulmasi sirasinda sanal makina baz imajlari ve kurulum paketleri internetten indirilecegi icin kurulum sirasinda internet erisimi gereklidir. Sistem kurulumu tamamlandiktan sonra, demo ortaminin kullanilmasi icin internet baglantisi gerekli degildir, istenirse kapatilabilir.

#### Git Kurulumu
Git debian paket depolarindan asagidaki komutla kurulabilir.
```bash
$ sudo apt-get install git
```

#### Vagrant Kurulumu

1. Debian turevleri icin (Pardus dahil) vagrant kurulumu : https://www.vagrantup.com/downloads.html adresinden indirilebilen https://releases.hashicorp.com/vagrant/2.1.2/vagrant_2.1.2_x86_64.deb(https://releases.hashicorp.com/vagrant/2.1.2/vagrant_2.1.2_x86_64.deb) paketi ile yapilabilir. Paket indirildikten sonra asagidaki komut ile kurulabilir:
```bash
$ sudo dpkg -i vagrant_2.1.2_x86_64.deb
```
2. Sanal makinalarin ve host uzerindeki /etc/hosts dosyalarinin provision sirasinda degistirilebilmesi icin, Vagrant'in [Hostmanager eklentisinin](https://github.com/devopsgroup-io/vagrant-hostmanager) kurulmasi gerekmektedir.
```bash
$ vagrant plugin install vagrant-hostmanager
```

#### Ansible Kurulumu

Debian turevleri icin (Pardus dahil) ansible kurulumu asagidaki adimlar ile yapilir:
1. Repo anahtarlari import edilir:
```bash
$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
```
2. Repo eklenir:(asagidaki ornek ubuntu 18.04 LTS icin verilmistir, diger debian turevleri icin gerekli degisiklik komut icinde yapilmalidir)
```bash
$ sudo apt-add-repository "deb http://ppa.launchpad.net/ansible/ansible/ubuntu bionic main"
```
3. Ansible kurulur:
```bash
$ apt-get install ansible
```
4. Kurulum test edilir:
```bash
$ ansible --version

ansible 2.7.0
  config file = /mnt/data1/la_vagrant_deployment/ansible.cfg
  configured module search path = [u'/home/ozgur/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.15rc1 (default, Apr 15 2018, 21:51:34) [GCC 7.3.0]
```

#### Virtualbox Kurulumu
1. Demo icin kullanilacak sistemde virtualbox kurulumu yapilmis olmalidir. Kurulum [virtualbox download](https://www.virtualbox.org/wiki/Linux_Downloads) sayfasindan indirilebilen [bionic paketi](https://download.virtualbox.org/virtualbox/5.2.16/virtualbox-5.2_5.2.16-123759~Ubuntu~bionic_amd64.deb) ile yapilir.
2. Virtualbox kurulduktan sonra yine [virtualbox download](https://www.virtualbox.org/wiki/Downloads) sayfasinda bulunan [extension paketi](https://download.virtualbox.org/virtualbox/5.2.16/Oracle_VM_VirtualBox_Extension_Pack-5.2.16.vbox-extpack) kurulur.


## Vagrant dosyasinin calistirilmasi
1. Sadece
```bash
$ vagrant up
```
komutu calistirilir ve kurulumun bitmesi beklenir. Kurulum sirasinda Virtualbox uygulamasi acilip, mevcut sanal makina listesi kontrol edilirse, LA bilesenlerine ait sanal makinalarin, Vagrantfile icindeki sira ile olustugu gorulebilir. Kurulum tamamlandiginda console makinasi virtualbox uzerinden acilarak 'vagrant' kullanici adi ve 'vagrant' sifresi ile kullanilabilir.


#### NOT:
Kurulan tum sanal makinalar icin kullanici adi ve sifre "vagrant" olarak olusturulmustur.
