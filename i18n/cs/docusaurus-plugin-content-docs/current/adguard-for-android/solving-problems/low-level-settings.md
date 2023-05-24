---
title: Průvodce nízkoúrovňových nastavení
sidebar_position: 6
---

## Jak dosáhnout nízkoúrovňových nastavení

> Změna *Nízkoúrovňových nastavení* může způsobit problémy s výkonem AdGuardu, může přerušit internetové připojení nebo ohrozit vaši bezpečnost a soukromí. Tuto část byste měli otevřít pouze v případě, že jste si jisti tím, co děláte, nebo pokud se vás na to zeptal náš tým podpory.

To go to *Low-level settings*, open the AdGuard app and tap the gear icon in the lower right corner of the screen. Then choose *General → Advanced → Low-level settings*.

## Nízkoúrovňová nastavení

For AdGuard v4.0 for Android we've completely redesigned the low-level settings: divided them into thematic blocks, made them clearer, added validation of entered values and other safety valves, got rid of some settings, and added others.

### DNS ochrana

#### Záložní odchozí připojení

Here you can specify the fallback DNS resolver(s) to be used if the configured server is unavailable. There are three options: *Automatic DNS*, *None*, and *Custom DNS*. If no fallback server is specified, the *Automatic DNS* — the system DNS or AdGuard DNS — will be used. *None* means no fallback at all. Selecting *Custom DNS* allows you to list IPv4 and IPv6 server addresses to use as upstreams.

#### Záložní domény

Here you can list domains that will be forwarded directly to fallback upstreams if they exist.

#### Detekce vyhledávacích domén

If this option is enabled, AdGuard will detect search domains and automatically forward them to fallback upstreams.

#### Odchozí bootstrap připojení

Bootstrap DNS pro servery DoH, DoT a DoQ. The *Automatic DNS* - the system DNS or AdGuard DNS - is used by default. By selecting *Custom DNS*, you can list IPv4 and IPv6 server addresses to use as bootstrap upstreams.

#### Režim blokování pro pravidla stylu adblock

Here you can specify the response type for domains blocked by DNS rules based on adblock rule syntax (for instance, `||example.org^`).

*  Respond with REFUSED (default)
*  Respond with NXDOMAIN
*  Respond with Custom IP address (IPv4 and IPv6 addresses can be specified here)

#### Režim blokování pro pravidla hosts

Here you can specify the response type for domains blocked by DNS rules based on hosts rule syntax (for instance, `<ip> <domain> 0.0.0.0 example.com`).

*  Respond with REFUSED
*  Respond with NXDOMAIN
*  Respond with Custom IP address (IPv4 and IPv6 addresses can be specified here) – default

#### Časový limit DNS požadavku

Zde můžete zadat dobu v milisekundách, po kterou bude AdGuard čekat na odezvu od vybraného DNS serveru, než se uchýlí k nouzovému řešení. Pokud toto pole nevyplníte nebo zadáte neplatnou hodnotu, bude použita hodnota 5000.

#### Blokovaná odezva TTL

Zde můžete zadat hodnotu TTL (time to live), která bude vrácena jako odpověď na zablokovaný požadavek.

#### Velikost mezipaměti DNS

Here you can specify the maximum number of cached responses. Default value is 1000.

#### Blokování ECH

If enabled, AdGuard strips Encrypted Client Hello parameters from DNS responses.

#### Ignorovat nedostupný odchozí proxy

Enable this feature to make AdGuard send DNS requests directly if the outbound proxy is unavailable.

#### Vyzkoušet HTTP/3 pro odchozí připojení DNS-over-HTTPS

By default, all DNS requests for DNS-over-HTTPS are sent via HTTP/2 protocol. If enabled, AdGuard uses HTTP/3 to speed up DNS query resolution for DoH upstreams.

#### Reakce na selhání SERVFAIL

Once enabled, AdGuard sends a SERVFAIL response to the client if all upstreams, including fallback ones, fail to reply. When this setting is disabled, no response is sent to the client.

#### Použít záložní řešení pro domény, které nejsou záložní

Enable this feature if you want AdGuard to use fallback upstream for all domains. Otherwise, fallback upstream will only be used for fallback domains and search domains if the corresponding option is enabled.

#### Ověřit odchozí připojení DNS

Enable to make AdGuard test DNS upstreams before adding or updating custom DNS servers.

### Filtrování

#### Zachytit HAR

Zde můžete povolit zachycení souboru HAR. Používejte to pouze pro účely ladění! Pokud je toto nastavení povoleno, AdGuard vytvoří adresář s názvem "har" uvnitř adresáře mezipaměti aplikace. Obsahuje informace o všech filtrovaných požadavcích HTTP ve formátu HAR 1.2 a lze je analyzovat pomocí programu Fiddler.

### HTTPS filtrování

#### Encrypted Client Hello

Každé šifrované internetové připojení má i nešifrovanou část. Jedná se o první paket, který obsahuje název serveru, ke kterému se připojujete. Technologie Encrypted Client Hello má tento problém vyřešit a zašifrovat poslední kousek nešifrovaných informací. Chcete-li to využít, povolte možnost *Encrypted ClientHello*. K vyhledání konfigurace ECH pro danou doménu používá místní proxy server DNS. Pokud je nalezen, paket ClientHello bude zašifrován.

#### Kontrola OCSP

Once enabled, this option runs asynchronous OCSP checks to check whether the website’s SSL certificate is revoked.

If the OCSP check is completed within the minimum timeout, AdGuard will immediately block the connection if the certificate is revoked or establish the connection if the certificate is valid.

If the verification takes too long, AdGuard will establish a connection and continue checking the certificate in the background. If it is revoked, current and future connections to the domain will be blocked.

#### Přesměrovat požadavky DNS skrze HTTPS

IF enabled, DNS-over-HTTPS requests will be redirected to the DNS Protection module. We recommend disabling fallback upstreams and use only encrypted DNS servers to maintain privacy.

### Odchozí proxy

#### Zobrazit nastavení "Filtrovat požadavky DNS"

When this feature is enabled, the string *Filter DNS requests* appears in the *Settings ➝ Filtering ➝ Network ➝ Proxy ➝ Proxy server ➝ Add proxy server* section with the switch next to it. By toggling the switch, you can enable filtering of DNS requests passing through the proxy.

### Ochrana

#### Rozsahy portů

Here you can specify port ranges that should be filtered.

#### Zaznamenat odstraněné HTML události

If enabled, AdGuard records blocked HTML elements in the filtering log.

#### Ladění skripletů

If you need to activate debugging of scriptlets, enable this feature. Then there will be messages in the browser log that some scriplet rules have been applied.

#### Vyloučené aplikace

Here you can list package names and UIDs that you want to exclude from AdGuard protection.

#### Obcházení balíčků QUIC

Here you can specify package names for which AdGuard should bypass QUIC traffic.

#### Reconfigure Automatic proxy when network changes

Enable this setting if you want the protection to restart to reconfigure the automatic proxy settings when the device connects to another network. The state of this setting affects operation only if the current routing mode is Automatic proxy.

#### Filtrování IPv6

If enabled, AdGuard filters IPv6 networks if an IPv6 network interface is available.

#### Rozsahy IPv4 vyloučené z filtrování

Filtering for IPv4 ranges, listed in this section, will be disabled.

#### Rozsahy IPv6 vyloučené z filtrování

Filtering for IPv6 ranges, listed in this section, will be disabled.

#### Zachování záznamů TCP pro odchozí sokety

If enabled, AdGuard sends a keepalive probe after the specified time period to ensure if the TCP connection is alive. Here you can specify the TCP keepalive idle time before starting keepalive probes and time between keepalive probes for an unresponsive peer.

After a system-defined number of unsuccessful attempts to get a response from the server, the system automatically closes the TCP connection.

### Nastavení lokální VPN

#### Zpoždění obnovy u odvolané VPN

Here you can set the time of a delay in milliseconds before AdGuard tries to restore VPN protection after it has been revoked by a third-party VPN app or by deleting the VPN profile. The default value is 5000 ms.

#### Zpoždění při změně plánu pro obnovení odvolané VPN

Here you can set the time of a delay in milliseconds before AdGuard reschedules the restoration of VPN protection after it has been revoked by a third-party VPN app or by deleting the VPN profile. The default value is 5000 ms.

#### MTU

Zde můžete nastavit maximální přenosovou jednotku (MTU) rozhraní VPN. The recommended range is 1500-1900 bytes.

#### Automatické obnovení VPN

If enabled, this feature automatically re-enables AdGuard’s local VPN after it has been turned off due to network absence, tethering, or low-power mode.

#### Zachycování paketů (PCAP)

If enabled, AdGuard will create the special file name `timestamp.pcap` (for instance, 1682599851461.pcap). Obsahuje všechny síťové pakety přenášené prostřednictvím VPN. Tento soubor se nachází v adresáři mezipaměti aplikace a lze jej analyzovat pomocí programu Wireshark.

#### Zahrnout bránu Wi-Fi v trasách VPN

If you want the gateway IP addresses to be added to VPN routes when on Wi-Fi, enable this feature.

#### Adresa IPv4

Here you can enter the IP address that will be used to create a TUN interface. By default, it is `172.18.11.218`.

#### Vynucené směrování LAN IPv4

When enabled, AdGuard filters all LAN connections, including local IPv4 network traffic, even if the *Route all LAN IPv4 connections* option is enabled.

#### Nucené směrování všech LAN IPv4

Once enabled, AdGuard excludes LAN connections from filtering for simple networks. May not work for complex networks. Works only with the *Forcibly route LAN IPv4* option disabled.

#### Adresa IPv6

Here you can enter the IP address that will be used to create a TUN interface. By default, it is `2001:db8:ad:0:ff::`.

### Různé

#### Detekce Samsung Pay

Korean users may encounter issues with Samsung Pay when AdGuard is enabled. Activate this feature to pause AdGuard's protection and use the Samsung Pay app seamlessly.
