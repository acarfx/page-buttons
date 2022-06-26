Discord.js kolay bir şekilde sayfa oluşturmak ister misin?
Hemde düğme şeklinde.

Yukarda bulunan Javascript dosyasını öncelikle botumuza çağırmamız gerek.
```js
const { Pages } = require('./_pages.js');
```
Şeklinde çağırabilirsiniz.

Örnek Olarak:
```
Pages(
  interaction,
  Array şeklinde sayfalar,
  Array şeklinde düğmeler,
  Embed ise "EMBED" sadece string ise "CONTENT",
  Düğmelerin deferleme süresi Varsayılan 120000,
  Embed ise aşağıda sayfa bilgisi açık ise true,
  Bitiş Sayfa Açık İse: true kapalı ise false,
  Bitiş Sayfa Numarası
);
```

Bu şekilde komut içerisine koyabilirsiniz ayrıca Slash komutları da desteklemektedir.

```js
  let sayfalar = [
        new genEmbed().setDescription("Birinci sayfam."),
        new genEmbed().setDescription("İkinci sayfam."),
        new genEmbed().setDescription("Üçüncü sayfam."),
        new genEmbed().setDescription("Dördüncü sayfam."),
        new genEmbed().setDescription("Beşinci sayfam."),
        new genEmbed().setDescription("Altıncı sayfam."),
        new genEmbed().setDescription("Bitiş sayfam."),
    ]
    let düğmeler = [
            new MessageButton()
                .setCustomId('geri')
                .setLabel('Geri')
                .setStyle('DANGER'),
            new MessageButton()
                .setCustomId('ileri')
                .setLabel('İleri')
                .setStyle('SECONDARY')
    ]
      let Row = new MessageActionRow().addComponents(
        new MessageButton()
            .setLabel("Sayfaları Görüntüle!")
            .setCustomId('test')
            .setStyle("PRIMARY")
    )
    message.reply({components: [Row], content: `Aşağıda ki düğme ile sayfaları görüntüleyebilirsin. **+**`}).then(msg => {
        var filter = (i) => i.user.id == message.author.id
        let collector = msg.createMessageComponentCollector(filter, {time: 120000});

        collector.on('collect', async (i) => {
            if (i.customId == 'test') {
                await Pages(i, sayfalar, düğmeler, "EMBED", 120000, true, true, 4);
            }
        })

        collector.on('end', async (collected, reason) => {
            if (reason == 'time') {
                message.reply('Zaman aşımına uğradın.')
            }
        })
    })
```
Bitişli sayfa görüntüsü:

![image](https://user-images.githubusercontent.com/77089894/175794235-8bbdfae0-798a-41c5-8e7d-560bc42b7f37.png)

Normal sayfa görüntüsü:

![image](https://user-images.githubusercontent.com/77089894/175794238-2cf4b348-4834-482e-ad45-12b015a2dfb8.png)

Yazı sayfa görüntüsü:

![image](https://user-images.githubusercontent.com/77089894/175794246-e3fee397-930a-473d-aa47-9adc8c30c2e8.png)

