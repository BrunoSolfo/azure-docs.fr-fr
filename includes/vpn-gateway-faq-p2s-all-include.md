### <a name="supportedclientos"></a>Quels systèmes d’exploitation client puis-je utiliser avec une connexion point à site ?

Les systèmes d’exploitation clients pris en charge sont les suivants :

* Windows 7 (32 bits et 64 bits)
* Windows Server 2008 R2 (64 bits uniquement)
* Windows 8 (32 bits et 64 bits)
* Windows 8.1 (32 bits et 64 bits)
* Windows Server 2012 (64 bits uniquement)
* Windows Server 2012 R2 (64 bits uniquement)
* Windows 10
* OSX version 10.11 pour Mac (El Capitan)
* MacOS version 10.12 pour Mac (Sierra)

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>Combien de points de terminaison clients VPN puis-je avoir dans ma configuration point à site ?

Nous prenons en charge jusqu'à 128 clients VPN pouvant se connecter à un réseau virtuel en même temps.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>Puis-je parcourir les serveurs proxy et les pare-feu à l’aide de la fonctionnalité point à site ?

Azure prend en charge deux types d’options de VPN point à site :

* Protocole SSTP (Secure Socket Tunneling Protocol)

  SSTP est une solution SSL propriétaire de Microsoft qui peut pénétrer les pare-feux, car la plupart des pare-feux ouvrent le port TCP 443 utilisé par SSL.

* VPN IKEv2

  Le VPN IKEv2 est une solution VPN IPsec basée sur des normes qui utilise les ports UDP 500 et 4500 ainsi que le protocole IP no. 50. Les pare-feux n’ouvrent pas toujours ces ports. Il est donc possible que le VPN IKEv2 ne soit pas en mesure de parcourir les proxies et pare-feux.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-the-vpn-automatically-reconnect"></a>Si je redémarre un ordinateur client avec une configuration point à site, le réseau VPN va-t-il se reconnecter automatiquement ?

Par défaut, l'ordinateur client ne rétablit pas automatiquement la connexion VPN.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-the-vpn-clients"></a>La configuration point à site prend-elle en charge la reconnexion automatique et DDNS sur les clients VPN ?

La reconnexion automatique et DDNS ne sont actuellement pas pris en charge dans les configurations VPN point à site.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-the-same-virtual-network"></a>Puis-je avoir des configurations coexistantes site à site et point à site pour un même réseau virtuel ?

Oui. Pour le modèle de déploiement Resource Manager, vous devez disposer d’un type de VPN basé sur le routage pour votre passerelle. Pour le modèle de déploiement Classic, vous avez besoin d’une passerelle dynamique. Nous ne prenons pas en charge la configuration point à site pour les passerelles VPN à routage statique ou les passerelles VPN basée sur une stratégie.

### <a name="can-i-configure-a-point-to-site-client-to-connect-to-multiple-virtual-networks-at-the-same-time"></a>Puis-je configurer un client point à site pour me connecter à plusieurs réseaux virtuels en même temps ?

Non. Un client point à site ne peut se connecter qu’aux ressources dans le réseau virtuel dans lequel réside la passerelle de réseau virtuel.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>Quel débit puis-je attendre des connexions site à site ou point à site ?

Il est difficile de maintenir le débit exact des tunnels VPN. IPsec et SSTP sont des protocoles VPN de chiffrement lourd. Le débit est également limité par la latence et la bande passante entre vos locaux et Internet. Pour une passerelle VPN ne disposant que des connexions VPN point à site IKEv2, le débit total que vous obtiendrez dépend de la référence SKU de passerelle. Pour plus d’informations sur le débit, consultez [Références SKU de passerelle](../articles/vpn-gateway/vpn-gateway-about-vpngateways.md#gwsku).

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp-andor-ikev2"></a>Puis-je utiliser un client VPN logiciel pour une connexion point à site prenant en charge SSTP et/ou IKEv2 ?

Non. Vous ne pouvez utiliser le client VPN natif sur Windows que pour SSTP et pour le client VPN natif sur Mac pour IKEv2. Reportez-vous à la liste des systèmes d’exploitation client pris en charge.