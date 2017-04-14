**Big number - Crypto - 150**

Enoncé :

```
Big number!!
```
[Sources](src/)

__Résolution :__

Dans les sources deux clés publiques sont disponibles ainsi que deux messages chiffrés.

Pour fer :

Extraction des infos de la clé publique :
```
openssl rsa -in publickey.pem -pubin -text -modulus

Public-Key: (2047 bit)
Modulus:
    6c:a8:41:78:43:d5:a6:2d:d3:af:37:e0:92:68:bc:
    [...]
    9c:c0:ee:e1:bf:9f:7d:f8:23:2b:cb:01:e3:ff:a8:
    31
Exponent: 65537 (0x10001)
Modulus=6CA8417843D5A62DD3AF37E09268BCD6D60E507C5E07427BD88D94D8C838312180723D2CE9DB0CAB533BBD5FBB08DE600168BFBCE197CC6F4ADAE9909034350B3E7BEB07EC0786578BBD4EEB1F2FB343E14FFF4B4446BA3AB35FFE0A076B9A21B73AAB3F2B2B30208D3ADE7AC8F4027D9758AEF91EBB9DA8A57CAF2AC145A6758D6580203C97DD1645F3D25F6B6AF34AE2DD51ABA6A376AE28C2007C4600AF265421DE289D07C4E69A445D2A99AAEF72BC1C08298E34CD495EDB7433EC02495435B2DFA23CD4EBAF5CF348D2AAF14512F450E90E081103071B07BB09DA8245572F30B1F455C454CE4ACD688FD59960549CC0EEE1BF9F7DF8232BCB01E3FFA831
-----BEGIN PUBLIC KEY-----
MIIBITANBgkqhkiG9w0BAQEFAAOCAQ4AMIIBCQKCAQBsqEF4Q9WmLdOvN+CSaLzW
[...]
9FDpDggRAwcbB7sJ2oJFVy8wsfRVxFTOSs1oj9WZYFScwO7hv599+CMrywHj/6gx
AgMBAAE=
-----END PUBLIC KEY-----
```

On passe le message chiffré en hexa :

```
cat message | xxd -p

166889f7c0fc8271d5a3ae780170959660c2f48a94eaed69b71fdb6c064c
f2c9446a10d9adb55c137c8c9ec2e3a68ae1913c0f98f3678d95a08fc3fd
538a170cdb3d834f66fa93f61561a9ebe6373927787268722bc8079ea447
53d98a1a5ece18fe68f4e4e04b590763a6239d6c7d458e1a81a1b4cb5fd5
f4183e25c39a8a1017ed8d9464adf7f95a0f833afc526d61a47486305440
f8bcd3caf758d2867b95c983421c01a5d13c429d5a210d1983ccd2cb3fdf
08c71d262deb962dc658639a404dd1f735c4ae64c9c4f522068b73434ce2
909a4c90bccd9946ec28816067d7635bb643eecdba1969d72932a060aece
36180c8542a44e0eb084020dd9e77df2

```

Nous avons donc n qui est notre modulo , e notre exposant et c notre chiffré.
On passe notre modulo et notre chiffré de l'hexa au décimal :
```PYTHON
int(n,16)
int(c,16)
```


Attaque de fermat :
```
./attackrsa -t fermat -n 13716706934727190104761352579820103471075035499949968745929609366488131317665912350255544005049294358736227634060531070214357544799001157339277520253151041651872341016789497066025690360174126918484351392893898453125147258404984071003233955922916388962361489111394732865053848535159397756031472820200814145642857568276942228629498348611333650603744183189426318246380780423083269692970865472117753612316437128324826535959393796599129018060105998398956736992084024570837511944117279282127860557751319463769809211712540979958922994810991333835423429068979054932716670749285014560009654280857008990452913472865388294285361 -e 65537 -c 2828792780224588153724014107149453660928611363779934083002843752469245430901174051085749251752796346717534660506060326976934353411294476430048385962397511850649981860368213494173689361981258664160584422736498495902131095769569039740891021403112963330680823644822715000963614883722786673128744624160624057412546238019540411386187765857850989456040433026989601760064197760970377254765157513996297043448710717977511239532002987928868151311962789687810084114363142823836289347081954134119243927520583540321119991032210810148695125847946744917357901735416443895613880722454419134289103789632964896345397761542288142990834

====== Cracked! =======
d is 0x3a47c5560c8c7c25f874f333b1541c75df3aae5106de3dfacf9ca149e59abe3f89f5bc7a6ab4e386c18e39752f8d0239dc87a2d05cf05ee712ef7877e1e11ed279215e5f516a77d45d4f9d14e01565c1f3084596c978664b360b36e78a335ce8d8aecf4b828c17b45e0c4568f6806b1592282f31d01a31e6535d1d5781732a651017eb34278e004d2d1e6ea31c51a2c46ce85e659795fddf6af3626693ef6daefc2368c854e11bf942345df8446dd23d96540364cef29f285a542db4fdfc0f2ec8fa1073f6a8ffb015cbe7280fce508d864c4b056b9fb0565f004764dd4327ddda24d926d88c0ff9541e87f850319147fb7404b3d0719b28dce0ac1a80454f5
p is 0xa6c8351fc7d43c0c6d82242422594f26d7b144ecb34aa98cff561da0ddd2c6a0698102ba97c6020c6b258f7be3b55767e30f343b29d433f96bbddd7da9631739929a3060a60f244d4a8370f3cba8fd8e678974945558ebd191294dd4075386fe153251f17afb6b84f60193b01deabededea57284b8fd616febcc29cdb04804c7
q is 0xa6c8351fc7d43c0c6d82242422594f26d7b144ecb34aa98cff561da0ddd2c6a0698102ba97c6020c6b258f7be3b55767e30f343b29d433f96bbddd7da9631739929a3060a60f244d4a8370f3cba8fd8e678974945558ebd191294dd4075386fe153251f17afb6b84f60193b01deabededea57284b8fd616febcc29cdb0480347
Plain text is 0x27204a7d8e25b5d604a748d0eb7662dedfefa7e2b6c0c61dc52c98370f2f60e7b93eef01a8f01c1c5db68b2e25631a253402c12697dc110755a91166a9c52d1106e46d2bf6804635938711846f0de8ee1cddc0bb8e239641e4884bbb94f6c947b068e9241a86da6fdce17a0a10fc91f3caf2ac2c1fd988b639af6cba87d242f7937ecbd6530479afc9fd99f48ff170bd41ee07979738ee0334a89f04e579d1563dad5a757ed5c55d368bebbc01353cf67fccbd2b6c17f2b0d0e261da200356330373065353831663165346131353265303430653237346237323437323034343563333133313265336531303262303530363763353733383230306430370a
```

p et q nous sont fournis en hexa , on les convertis en int 

int(p,16)
int(q,16)

On génère ensuite notre clé privé :

```
python rsatool.py -p 117118345850371324755442721691010370746296466217613601391163655840990077599670230417096624741289813886405031113346503009135170495702881435092555492730582477110270806706808191842281165589328069923809725129015935929853235145002864445534915392828344509262317077113013662247163187898805965856003962565368895505607 -q 117118345850371324755442721691010370746296466217613601391163655840990077599670230417096624741289813886405031113346503009135170495702881435092555492730582477110270806706808191842281165589328069923809725129015935929853235145002864445534915392828344509262317077113013662247163187898805965856003962565368895505223 -f PEM -o privfit_fer.pem
```
On déchiffre notre message chiffré :
```
openssl rsautl -decrypt -inkey privfit_fer.pem -in message > decrypt_fer
```
On affiche le résultat :
```
cat decrypt_fer

5c070e581f1e4a152e040e274b724720445c31312e3e102b05067c5738200d07
```

Pour seru :

Extraction des infos de la clé publique :
```
openssl rsa -in publickey.pem -pubin -text -modulus

Public-Key: (7470 bit)
Modulus:
    3f:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    [...]
    00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:
    00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:
    00:00:00:01
Exponent: 65537 (0x10001)
Modulus=3FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF[...]00000000000000000001
-----BEGIN PUBLIC KEY-----
MIIDxzANBgkqhkiG9w0BAQEFAAOCA7QAMIIDrwKCA6Y/////////////////////
[...]
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAABAgMBAAE=
-----END PUBLIC KEY-----
```

On passe le message chiffré en hexa :

```
cat message | xxd -p

3d2a2d546ccf01f188a31617b47c0fcee983956d6f764028439b498b2a09
13c587d877ed1dd1847306d69029e5c111ff2f88a50ea7b0ce7969ba1ce4
ea3703c774dffb739515b304ae28aa0e9940709a7cd203e53ecea91bc957
f909cbb4ca346ce906d08604af5af9d463e55b1e2c4c293fe36b11a48a3e
7f94d6ab3e3f803d3776b0fd1298194103bc34db272c31045f2777f7b846
916572a1e77e8b28e6fc34b04a0720286b79a97d84241f7a012344134fb9
[...]
```
Nous avons donc n qui est notre modulo , e notre exposant et c notre chiffré.
On passe notre modulo et notre chiffré de l'hexa au décimal :
```PYTHON
int(n,16)
int(c,16)
```

On trouve les facteurs de n sur [factor-db](http://factordb.com/) :

```
p=2^4253-1
q=2^3217-1
```

On reconstruit notre clé privé :
```
python rsatool.py -p 190797007524439073807468042969529173669356994749940177394741882673528979787005053706368049835514900244303495954950709725762186311224148828811920216904542206960744666169364221195289538436845390250168663932838805192055137154390912666527533007309292687539092257043362517857366624699975402375462954490293259233303137330643531556539739921926201438606439020075174723029056838272505051571967594608350063404495977660656269020823960825567012344189908927956646011998057988548630107637380993519826582389781888135705408653045219655801758081251164080554609057468028203308718724654081055323215860189611391296030471108443146745671967766308925858547271507311563765171008318248647110097614890313562856541784154881743146033909602737947385055355960331855614540900081456378659068370317267696980001187750995491090350108417050917991562167972281070161305972518044872048331306383715094854938415738549894606070722584737978176686422134354526989443028353644037187375385397838259511833166416134323695660367676897722287918773420968982326089026150031515424165462111337527431154890666327374921446276833564519776797633875503548665093914556482031482248883127023777039667707976559857333357013727342079099064400455741830654320379350833236245819348824064783585692924881021978332974949906122664421376034687815350484991 -q 259117086013202627776246767922441530941818887553125427303974923161874019266586362086201209516800483406550695241733194177441689509238807017410377709597512042313066624082916353517952311186154862265604547691127595848775610568757931191017711408826252153849035830401185072116424747461823031471398340229288074545677907941037288235820705892351068433882986888616658650280927692080339605869308790500409503709875902119018371991620994002568935113136548829739112656797303241986517250116412703509705427773477972349821676443446668383119322540099648994051790241624056519054483690809616061625743042361721863339415852426431208737266591962061753535748892894599629195183082621860853400937932839420261866586142503251450773096274235376822938649407127700846077124211823080804139298087057504713825264571448379371125032081826126566649084251699453951887789613650248405739378594599444335231188280123660406262468609212150349937584782292237144339628858485938215738821232393687046160677362909315071 -f PEM -o privfit_seru.pem
```

On déchiffre notre message chiffré :
```
openssl rsautl -decrypt -inkey privfit_seru.pem -in message > decrypt_seru
```
On affiche le résultat :
```
cat decrypt_seru

65417439774c784d56415a44784b76423265775257736a7369374e326d4c6655
```

On xor les deux chaines trouvés avec xorstrings :

```
python xorstrings.py 5c070e581f1e4a152e040e274b724720445c31312e3e102b05067c5738200d07 65417439774c784d56415a44784b76423265775257736a7369374e326d4c6655
39467a6168523258784554633339316276394663794d7a586c313265556c6b52
```

On passe ensuite de l'hexa au base64 et on le decode :

```PYTHON
import binascii
import base64

xor="39467a6168523258784554633339316276394663794d7a586c313265556c6b52"

chaineB64=binascii.unhexlify(xor)

revchaineB64=chaineB64[::-1]

print base64.b64decode(revchaineB64)
```

Le flag était :
```
FIT{me_32p_oo_wq11_dak1}
```

By team Beers4Flags


```
 ________
|        |
|  #BFF  |
|________|
   _.._,_|,_
  (      |   )
   ]~,"-.-~~[
 .=] Beers ([
 | ])  4   ([
 '=]) Flags [
   |:: '    |
    ~~----~~
```