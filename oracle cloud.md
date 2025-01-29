


# Puntos a tener en cuenta al crear instancia
## Como Habilitar los puertos 80 y 443 ?
>
 1. Virtual cloud networks-Default Security List for 
 2. Ingresar a la instancia y actualizar el iptable.
> 
> nano /etc/iptables/rules.v4

    Agregar al archivo rules.v4 las siguientes lineas

> -A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT \
> -A INPUT -p tcp -m state --state NEW -m tcp --dport 443 -j ACCEPT

`Comando para actualizar iptable `

> iptables-restore < /etc/iptables/rules.v4
 3. Validar si los puertos están en escucha
>ss -nltp
 4. Agregar la Ip de la instancia en cloudflare y posteriormente validar la propagacion de la Ip
 [Comprobador de propagación DNS](https://whatsmydns.me/es#A/www.lgyss.click)
 5. Video youtube  [fixing_access_issues_open_ports_on_oracle_clouds](Agregar%20la%20Ip%20de%20la%20instancia%20en%20cloudflare%20y%20posteriormente%20validar%20la%20propagacion%20de%20la%20Ip%20%20%5BComprobador%20de%20propagaci%C3%B3n%20DNS%5D%28https://whatsmydns.me/es#A/www.lgyss.click%29)
 
## Instalar docker
> sudo apt update \
> sudo apt upgrade -y \
> curl -fsSL https://get.docker.com -o get-docker.sh \
> sudo sh get-docker.sh

