# encrypt-fragment

# 原版官方网站

http://travistidwell.com/jsencrypt

# 介绍

基于 jsencrypt 扩展分段加解密功能

npm 安装：

```bash
npm i encrypt-fragment -S
```

浏览器使用：

```html
开发：<script src="./bin/jsencrypt.js"></script>
生产：<script src="./bin/jsencrypt.min.js"></script>
```

# 基本使用



> 注意：使用长文本加密时最好公私钥都要设置，避免有概率加密失败

这里只扩展了长文本的分段加解密，其它 api 请查看官网 http://travistidwell.com/jsencrypt

-   `encryptLong()` 长文本加密
-   `decryptLong()` 长文本解密

## DEMO

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <title>使用jsencrypt执行长文本分段加密，解密</title>
    </head>

    <body>
        <input type="button" id="btn" value="点我" />
        <span>F12打开开发者工具查看加解密结果</span>
        <div>密钥长度</div>
        <input
            id="key-size"
            value="512"
            type="text"
            placeholder="enter key size:(512 or 1024 or 2048 or 4096)"
        />
        <div>公钥</div>
        <textarea id="tra" rows="15" cols="65">
MFwwDQYJKoZIhvcNAQEBBQADSwAwSAJBAKjtJW+PjF4B9xPgAi0fchR38vxwoW8tJe473bRBo8Yhpz23akPo1hmLrC8syR9xhiLF6RFb601mY8uKxHC9KNsCAwEAAQ==</textarea
        >
        <div>私钥</div>
        <textarea id="sra" rows="15" cols="65">
MIIBVgIBADANBgkqhkiG9w0BAQEFAASCAUAwggE8AgEAAkEAqO0lb4+MXgH3E+ACLR9yFHfy/HChby0l7jvdtEGjxiGnPbdqQ+jWGYusLyzJH3GGIsXpEVvrTWZjy4rEcL0o2wIDAQABAkBx01nmUlPDBI/4VHki7o1wPWL9tucQgtuMK8q4K4KvfeUPqx3gSN/VEtS9SZpz1/yyRQNe7EY2ybxLVJRHdlQBAiEA2y3sJbOSGjiYvV5nA5XDDkGg/2OnD6VBDkyHVqRF9RcCIQDFTgfZpUMRx8wa32/t/kI4v1843gh99TlxkjVVJjCM3QIhAMpLMFH70zVwV0kxAFNGvqlB2Z7eEytVkx3ndGJ7bDYxAiEAh6qC3VW0S1qNboDqjsPAtxJnoEuTnUBr8jqtb1ImGgUCIQCY+5Wuakxho/jpa0Jwy4APpUBSniE9koN9i4qFCJBtvA==</textarea
        >
    </body>
    <style>
        #key-size {
            min-width: 300px;
        }
    </style>
    <script src="./jquery.js"></script>
    <!--引入jsencrypt.js-->
    <script src="./bin/jsencrypt.js"></script>
    <script type="text/javascript">
        document.getElementById('btn').addEventListener('click', () => {
            let startTime = new Date();

            // 使用设置公私钥
            const enc = new JSEncrypt({
                default_key_size:
                    Number(document.getElementById('key-size').value) || 1024
            });
            enc.setPublicKey(document.getElementById('tra').value);
            enc.setPrivateKey(document.getElementById('sra').value);

            // 一段长文本json
            let data = {
                code: 200,
                result: {
                    timestamp: 1572321851823,
                    interaction: [
                        {
                            type: 'shootYourBullet',
                            body: '{"actId":"241532192085135360","timestamp":1572321762049,"actTempId":"2","queIds":["10020"],"actTime":60,"online_trace_id":null}',
                            liveId: 100066318,
                            lecturerId: 'XN014604',
                            tutorId: 'XN014606',
                            parentType: 'interaction',
                            module: 'START',
                            command: 'START',
                            stuId: null,
                            online_trace_id: 'fhCb3oVqjM'
                        }
                    ],
                    upStream: {},
                    downStream: {},
                    liveStream: []
                }
            };
            let data1 = [
                {
                    _id: '62e7d0b6d90991e828fcee61',
                    index: 0,
                    guid: '3a85e6e2-5d68-446c-8382-152ecd795b75',
                    isActive: true,
                    balance: '$2,790.69',
                    picture: 'http://placehold.it/32x32',
                    age: 36,
                    eyeColor: 'green',
                    name: 'Craft Terrell',
                    gender: 'male',
                    company: 'FRANSCENE',
                    email: 'craftterrell@franscene.com',
                    phone: '+1 (835) 467-3075',
                    address: '528 Crescent Street, Bellfountain, Ohio, 4527',
                    about: 'Excepteur anim incididunt labore voluptate aute veniam magna magna laborum reprehenderit. Duis ea amet quis et cillum elit sint. Culpa et incididunt incididunt consectetur ipsum. Magna eu cupidatat reprehenderit ex Lorem nulla velit adipisicing laboris ex ut fugiat proident mollit. Duis duis adipisicing est elit enim culpa occaecat elit dolor irure ipsum officia.\r\n',
                    registered: '2018-01-24T05:57:35 -08:00',
                    latitude: 15.136309,
                    longitude: -12.324875,
                    tags: [
                        'deserunt',
                        'aute',
                        'est',
                        'ad',
                        'officia',
                        'anim',
                        'exercitation'
                    ],
                    friends: [
                        {
                            id: 0,
                            name: 'Faith Hampton'
                        },
                        {
                            id: 1,
                            name: 'Oneil Woods'
                        },
                        {
                            id: 2,
                            name: 'Marci Mccray'
                        }
                    ],
                    greeting:
                        'Hello, Craft Terrell! You have 10 unread messages.',
                    favoriteFruit: 'apple'
                },
                {
                    _id: '62e7d0b6fa33c962df1a8530',
                    index: 1,
                    guid: '77b1ed38-2ef5-403b-9425-b7736ce46a0a',
                    isActive: true,
                    balance: '$2,356.87',
                    picture: 'http://placehold.it/32x32',
                    age: 32,
                    eyeColor: 'brown',
                    name: 'Carroll Sears',
                    gender: 'male',
                    company: 'TINGLES',
                    email: 'carrollsears@tingles.com',
                    phone: '+1 (814) 433-2521',
                    address: '117 Rutledge Street, Walland, Maine, 2459',
                    about: 'Non velit enim nisi eiusmod nisi nulla aute occaecat Lorem. Nostrud proident minim velit proident laborum nostrud cillum nisi. Ut pariatur consectetur dolore proident ad elit consequat. Proident Lorem dolor veniam tempor ut amet laboris. Deserunt deserunt Lorem reprehenderit exercitation esse proident nisi sint. Reprehenderit sunt reprehenderit laboris occaecat veniam.\r\n',
                    registered: '2019-12-17T05:27:49 -08:00',
                    latitude: 69.066789,
                    longitude: 121.414055,
                    tags: [
                        'duis',
                        'Lorem',
                        'amet',
                        'proident',
                        'aliqua',
                        'est',
                        'incididunt'
                    ],
                    friends: [
                        {
                            id: 0,
                            name: 'Woodard Hensley'
                        },
                        {
                            id: 1,
                            name: 'Queen Dickson'
                        },
                        {
                            id: 2,
                            name: 'Robyn Hess'
                        }
                    ],
                    greeting:
                        'Hello, Carroll Sears! You have 7 unread messages.',
                    favoriteFruit: 'banana'
                },
                {
                    _id: '62e7d0b68b78f172fda4ea94',
                    index: 2,
                    guid: '42fa4c56-5acd-48c6-a248-18e37beae131',
                    isActive: false,
                    balance: '$3,112.91',
                    picture: 'http://placehold.it/32x32',
                    age: 33,
                    eyeColor: 'green',
                    name: 'Calderon Chen',
                    gender: 'male',
                    company: 'APPLIDECK',
                    email: 'calderonchen@applideck.com',
                    phone: '+1 (849) 513-2465',
                    address: '264 Schweikerts Walk, Lynn, Alabama, 1193',
                    about: 'Excepteur exercitation velit consequat excepteur aliquip ad qui ad magna fugiat nisi adipisicing. Incididunt officia proident magna id eiusmod nulla amet tempor culpa magna minim amet id occaecat. Dolor cupidatat exercitation amet qui magna duis cupidatat. Non do mollit consectetur ut deserunt irure adipisicing eiusmod non quis cillum dolor.\r\n',
                    registered: '2018-01-07T11:52:58 -08:00',
                    latitude: -17.74708,
                    longitude: 179.666975,
                    tags: [
                        'ea',
                        'aute',
                        'fugiat',
                        'nostrud',
                        'commodo',
                        'mollit',
                        'cupidatat'
                    ],
                    friends: [
                        {
                            id: 0,
                            name: 'Bender Snyder'
                        },
                        {
                            id: 1,
                            name: 'Clara Holt'
                        },
                        {
                            id: 2,
                            name: 'Carmella Solis'
                        }
                    ],
                    greeting:
                        'Hello, Calderon Chen! You have 2 unread messages.',
                    favoriteFruit: 'banana'
                },
                {
                    _id: '62e7d0b661c2c4be164c89f4',
                    index: 3,
                    guid: 'e55f8857-3536-4e36-8383-9070f7569c7d',
                    isActive: false,
                    balance: '$3,661.12',
                    picture: 'http://placehold.it/32x32',
                    age: 23,
                    eyeColor: 'brown',
                    name: 'Mclaughlin Carrillo',
                    gender: 'male',
                    company: 'ANIMALIA',
                    email: 'mclaughlincarrillo@animalia.com',
                    phone: '+1 (935) 568-2208',
                    address: '141 Frank Court, Richmond, Texas, 7846',
                    about: 'Proident velit amet dolor minim irure aute consectetur ea incididunt in fugiat esse. Reprehenderit quis labore minim labore pariatur eiusmod sit. Deserunt eiusmod exercitation id do nostrud ex non sint. Eiusmod in excepteur fugiat cupidatat id incididunt ad. Minim et adipisicing commodo enim. Ut voluptate ea deserunt ut magna deserunt aute Lorem ad non enim. Enim ea do ea eiusmod aliquip consectetur tempor enim ex officia ea et.\r\n',
                    registered: '2021-06-03T06:19:21 -08:00',
                    latitude: 14.9813,
                    longitude: 54.022948,
                    tags: [
                        'minim',
                        'aliquip',
                        'irure',
                        'cillum',
                        'nulla',
                        'sint',
                        'commodo'
                    ],
                    friends: [
                        {
                            id: 0,
                            name: 'Kelley Huber'
                        },
                        {
                            id: 1,
                            name: 'Raquel Hansen'
                        },
                        {
                            id: 2,
                            name: 'Rollins Oneal'
                        }
                    ],
                    greeting:
                        'Hello, Mclaughlin Carrillo! You have 7 unread messages.',
                    favoriteFruit: 'banana'
                },
                {
                    _id: '62e7d0b6fdf9b2e14e312e04',
                    index: 4,
                    guid: '1e4d4eb3-6249-49bc-9277-3a99d88f29d1',
                    isActive: true,
                    balance: '$3,826.78',
                    picture: 'http://placehold.it/32x32',
                    age: 22,
                    eyeColor: 'green',
                    name: 'Summer Grimes',
                    gender: 'female',
                    company: 'BLUEGRAIN',
                    email: 'summergrimes@bluegrain.com',
                    phone: '+1 (935) 571-3021',
                    address: '220 Ludlam Place, Shelby, Connecticut, 9246',
                    about: 'Consectetur Lorem ea laborum fugiat reprehenderit consectetur ea deserunt duis et. Do Lorem est non adipisicing ullamco aliquip duis ipsum ex dolor ad aliquip sint. Aliqua nisi qui amet duis nisi tempor tempor consequat incididunt. Pariatur incididunt minim aliqua est aliqua pariatur id ad. Dolore sunt consectetur ea do velit ut non dolore sunt duis minim est sint commodo.\r\n',
                    registered: '2020-08-31T07:20:28 -08:00',
                    latitude: -77.90575,
                    longitude: 137.082648,
                    tags: [
                        'cupidatat',
                        'id',
                        'non',
                        'adipisicing',
                        'eiusmod',
                        'ea',
                        'amet'
                    ],
                    friends: [
                        {
                            id: 0,
                            name: 'Manuela Gonzalez'
                        },
                        {
                            id: 1,
                            name: 'Kay Campbell'
                        },
                        {
                            id: 2,
                            name: 'Abbott Reilly'
                        }
                    ],
                    greeting:
                        'Hello, Summer Grimes! You have 10 unread messages.',
                    favoriteFruit: 'strawberry'
                }
            ];
            
            let encrypted = enc.encryptLong(JSON.stringify(data));
            let endTime = new Date();
            console.log('加密后数据:%o', encrypted);
            console.log('加密时间' + (endTime - startTime) + 'ms');
            //使用私钥解密
            let uncrypted = enc.decryptLong(encrypted);
            console.log('解密后数据:%o', uncrypted);
        });
    </script>
</html>
```
