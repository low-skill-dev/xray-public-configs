# Настройки v2ray для РФ
android: https://github.com/2dust/v2rayNG<br/>
windows: https://github.com/2dust/v2rayN<br/>
linux: https://github.com/v2rayA/v2rayA<br/>
ios: streisand, foxray

Однажды хамниг гуэй поспорил что напишет удобный JSON-формат конфигурирования прокси, но потом сделает для него такой GUI, чтобы все обплевались. Он выиграл спор.

### DNS
По неизвестной причине, запросы к DNS у v2ray идут весьма медленно. Поэтому RU зону гоним в тындыкс, весь DoH в direct. В прокси улетают только обычные dns типа 8.8.8.8.
```json
{"servers":[{"address":"https://77.88.8.8/dns-query","domains":["geosite:VK","geosite:YANDEX","geosite:MAILRU","regexp:.*\\.(ru|рф|by|kz|ir|dz|ar|af|bh|ba|bw|br|ve|vn|hk|eg|zw|il|in|id|jo|iq|ke|cn|kp|cr|kw|lb|ls|mu|mg|my|mv|ma|mz|md|mn|mm|na|om|pk|pe|sa|sc|rs|sy|th|tz|tn|tr|uy|fj|ph|lk|et|za|jm|az|am|kg|tj|tm|uz|bd|qa|cu|ae)$"]},{"address":"77.88.8.8","domains":["geosite:VK","geosite:YANDEX","geosite:MAILRU","regexp:.*\\.(ru|рф|by|kz|ir|dz|ar|af|bh|ba|bw|br|ve|vn|hk|eg|zw|il|in|id|jo|iq|ke|cn|kp|cr|kw|lb|ls|mu|mg|my|mv|ma|mz|md|mn|mm|na|om|pk|pe|sa|sc|rs|sy|th|tz|tn|tr|uy|fj|ph|lk|et|za|jm|az|am|kg|tj|tm|uz|bd|qa|cu|ae)$"]},"https://208.67.222.222/dns-query","https://8.8.8.8/dns-query","https://1.1.1.1/dns-query","https://9.9.9.9/dns-query","208.67.222.222","8.8.8.8","1.1.1.1","9.9.9.9"]}
```

### Routing
**4 апреля 2022 года Михаил Мишустин заявил об открытии авиасообщения с 52 дружественными странами:**<br/>
Алжир, Аргентина, Афганистан, Бахрейн, Босния и Герцеговина, Ботсвана, Бразилия, Венесуэла, Вьетнам, Гонконг, Египет, Зимбабве, Израиль, Индия, Индонезия, Иордания, Ирак, Кения, Китай, КНДР, Коста-Рика, Кувейт, Ливан, Лесото, Маврикий, Мадагаскар, Малайзия, Мальдивы, Марокко, Мозамбик, Молдова, Монголия, Мьянма, Намибия, Оман, Пакистан, Перу, Саудовская Аравия, Сейшелы, Сербия, Сирия, Таиланд, Танзания, Тунис, Турция, Уругвай, Фиджи, Филиппины, Шри-Ланка, Эфиопия, ЮАР, Ямайка.

**21 сентября 2023 года Правительство утвердило перечень стран, банки которых смогут ... в России:**<br/>
Азербайджан, Армения, Белоруссия, Киргизия, Таджикистан, Туркмения, Узбекистан, Алжир, Бангладеш, Бахрейн, Бразилия, Венесуэла, Вьетнам, Египет, Индия, Индонезия, Иран, Казахстан, Катар, Китай, Куба, Малайзия, Марокко, Монголия, ОАЭ, Оман, Пакистан, Саудовская Аравия, Сербия, Таиланд, Турция, ЮАР.

**Коды ISO 3166 этих "дружественных" стран:**<br/>
DZ, AR, AF, BH, BA, BW, BR, VE, VN, HK, EG, ZW, IL, IN, ID, JO, IQ, KE, CN, KP, CR, KW, LB, LS, MU, MG, MY, MV, MA, MZ, MD, MN, MM, NA, OM, PK, PE, SA, SC, RS, SY, TH, TZ, TN, TR, UY, FJ, PH, LK, ET, ZA, JM, AZ, AM, BY, KG, TJ, TM, UZ, BD, IR, KZ, QA, CU, AE.

Итого, напрямую гоним торрент, весь DoH, запросы к RU зоне и "дружественным странам", вотсап и телегу. Рекламу и телеметрию в блок. Остальное в прокси.
```json
[{"outboundTag":"direct","protocol":["bittorrent"],"remarks":"bittorrent"},{"outboundTag":"direct","ip":["geoip:private"],"remarks":"private"},{"outboundTag":"direct","domain":["geosite:private"],"remarks":"private"},{"outboundTag":"direct","ip":["77.88.8.8"],"remarks":"ya-dns"},{"outboundTag":"direct","ip":["208.67.222.222","77.88.8.8","9.9.9.9","8.8.8.8","1.1.1.1"],"protocol":["tls"],"remarks":"doh"},{"outboundTag":"block","domain":["geosite:category-ads-all"],"remarks":"ads"},{"outboundTag":"direct","domain":["regexp:.*\\.(ru|рф|by|kz|ir|dz|ar|af|bh|ba|bw|br|ve|vn|hk|eg|zw|il|in|id|jo|iq|ke|cn|kp|cr|kw|lb|ls|mu|mg|my|mv|ma|mz|md|mn|mm|na|om|pk|pe|sa|sc|rs|sy|th|tz|tn|tr|uy|fj|ph|lk|et|za|jm|az|am|kg|tj|tm|uz|bd|qa|cu|ae)$"],"remarks":"friendly-to-russia"},{"outboundTag":"direct","domain":["geosite:VK","geosite:YANDEX","geosite:MAILRU"],"remarks":"friendly-to-russia"},{"outboundTag":"direct","domain":["geosite:WHATSAPP","geosite:TELEGRAM"],"remarks":"social-networks"},{"outboundTag":"direct","ip":["geoip:ru","geoip:by","geoip:kz","geoip:ir","geoip:cn","geoip:ba","geoip:bw","geoip:br","geoip:ve","geoip:vn","geoip:hk","geoip:eg","geoip:zw","geoip:il","geoip:in","geoip:id","geoip:jo","geoip:iq","geoip:ke","geoip:bh","geoip:kp","geoip:cr","geoip:kw","geoip:lb","geoip:ls","geoip:mu","geoip:mg","geoip:my","geoip:mv","geoip:ma","geoip:mz","geoip:md","geoip:mn","geoip:mm","geoip:na","geoip:om","geoip:pk","geoip:pe","geoip:sa","geoip:sc","geoip:rs","geoip:sy","geoip:th","geoip:tz","geoip:tn","geoip:tr","geoip:uy","geoip:fj","geoip:ph","geoip:lk","geoip:et","geoip:za","geoip:jm","geoip:az","geoip:am","geoip:dz","geoip:kg","geoip:tj","geoip:tm","geoip:uz","geoip:bd","geoip:af","geoip:ar","geoip:qa","geoip:cu","geoip:ae"],"remarks":"friendly-to-russia"},{"port":"0-65535","outboundTag":"proxy","remarks":"other"}]
```
