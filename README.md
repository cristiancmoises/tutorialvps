# Tutorial - VPS
[![DOI](https://zenodo.org/badge/530124532.svg)](https://doi.org/10.5281/zenodo.14810240)  
## VPS + TOR + SSH + DNS (QUAD9) + FAIL2BAN) + IPTABLES + NFTABLES

Do you can use Let's Cloud or another VPS! FREE: https://hax.co.id/

    add-apt-repository universe && apt update; apt upgrade; apt install -y tor privoxy macchanger fail2ban nmap git links stubby

## STUBBY (QUAD9)
    mv /etc/stubby/stubby.yml /etc/stubby/stubby.backup.yml && sudo wget -O /etc/stubby/stubby.yml https://support.quad9.net/hc/en-us/article_attachments/4411087149453/stubby.yml
    service stubby restart
    service stubby status

## CLEAN (Clean temp files)
    git clone https://github.com/cristiancmoises/cleanall
    crontab -e
    * * * * * /root/clearner.sh
    grep CRON /var/log/syslog
    service rsyslog restart

## TOR
    apt install tor macchanger secure-delete -y
    git clone https://github.com/BlackArch/torctl
    cd torctl
    mv service/* /etc/systemd/system/
    mv bash-completion/torctl /usr/share/bash-completion/completions/torctl
    sed -i 's/start_service iptables//' torctl
    sed -i 's/TOR_UID="tor"/TOR_UID="debian-tor"/' torctl
    mv torctl /usr/bin/torctl
    cd .. && rm -rf torctl/
    torctl --h

## SSH
    nano /etc/ssh/sshd_config
##### change the default port

## FAIL2BAN
    cd /etc/fail2ban
    cp jail.conf jail.local
    nano jail.local
#### change the ssh port

## FIREWALL
    iptables -P INPUT DROP
    iptables -P FORWARD DROP
    iptables -P OUTPUT ACCEPT
    iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
    iptables -A INPUT -p tcp --dport 5000 -j ACCEPT
    iptables -A FORWARD  -p tcp --dport 80 -j ACCEPT
    iptables -A FORWARD  -p tcp --dport 443 -j ACCEPT
    iptables -A FORWARD  -p tcp --dport 8118 -j ACCEPT
    iptables -A FORWARD  -p tcp --dport 9050 -j ACCEPT
    iptables -A FORWARD -p tcp --dport 53 -j ACCEPT
    iptables -A FORWARD -p tcp --dport 5000 -j ACCEPT
    iptables -A OUTPUT -p tcp --dport 80 -j ACCEPT
    iptables -A OUTPUT -p tcp --dport 443 -j ACCEPT
    iptables -A OUTPUT -p tcp --dport 8118 -j ACCEPT
    iptables -A OUTPUT -p tcp --dport 9050 -j ACCEPT
    iptables -A OUTPUT -p tcp --dport 53 -j ACCEPT
    iptables -A OUTPUT -p tcp --dport 5000 -j ACCEPT

## HOSTS
    git clone https://github.com/cristiancmoises/hosts
    cd hosts
    rm -rf /etc/hosts && cp hosts /etc/hosts

## DNS
    nano /etc/resolv.conf
    nameserver 9.9.9.9
    nameserver 149.112.112.112
    chattr +i /etc/resolv.conf

## MANAGEMENT
    git clone https://github.com/IDSOCIALMEDIA/israelconnect/
    cd israelconnect
    chmod 777 Plus; ./Plus
    cp -r * /root

# TRANSFER.SH:
    curl --upload-file arquivo.txt https://transfer.sh/seuarquivo.txt
----------------------------------------------
### FREENOM - Free Domain:
    https://www.freenom.com/en/index.html?lang=en
---------------------------------------------
### CLOUDFLARE:
    https://dash.cloudflare.com
---------------------------------------------
### DNS - QUAD9:
    https://support.quad9.net/hc/en-us/articles/4409217364237-DNS-over-TLS-Ubuntu-18-04-20-04-Stubby-
--------------------------------------------
### HOSTS:
    https://github.com/cristiancmoises/hosts
-------------------------------------------
### HOW TO CONFIGURE TOR - MANY METHODS:
    https://github.com/BlackArch/torctl
    https://miloserdov.org/?p=3797
------------------------------------------
### Convert IPTABLES into NFTABLES:
    https://forums.linuxmint.com/viewtopic.php?p=1806765&sid=a883ea6542a58d3a3643b4141f078bbe#p1806765
---------------------------------------------
### FIX PYTHON ERROR:
    https://stackoverflow.com/questions/56218562/how-to-fix-modulenotfounderror-no-module-named-apt-pkg
---------------------------------------------
### LOGIN WITH PASSWORD:
    ssh-keygen   (rodar na maquina local)
    ssh-copy-id -p 5000 root@nomedohost
    ssh -p 5000 'root@nomedohost'
### Read More:
    https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server
---------------------------------------------
