
# ðŸ’¬ Discord.js Components V2 - Beginner Friendly Guide (Hinglish Style)

Components v2 is Discord ka naya message layout system, jo aapko **poora control** deta hai ki message ka layout kaise dikhe. Ye traditional `embed` system se zyada powerful aur flexible hai.

---

## ðŸš€ Kya Naya Hai Components V2 Mein?

- âš’ï¸ Fully customizable layouts (LEGO-style blocks)
- ðŸ“ Rich text with markdown
- ðŸŽ¨ Clean UI with sections, images, and spacing
- ðŸ”˜ Buttons & dropdowns included
- â— `content`, `embeds`, `stickers` nahi chalenge jab aap `MessageFlags.IsComponentsV2` use karoge

---

## ðŸ§± Basic Building Blocks

| Component | Use Kaha Hota Hai? |
|----------|-------------------|
| `ContainerBuilder` | Sabse outer layout banata hai |
| `TextDisplayBuilder` | Text likhne ke liye (markdown support) |
| `SectionBuilder` | Text + Button ko group karne ke liye |
| `SeparatorBuilder` | Gap ya divider line banane ke liye |
| `MediaGalleryBuilder` | Images, videos, GIFs dikhane ke liye |
| `FileBuilder` | File attachments dikhane ke liye |
| `ActionRowBuilder` | Button ya Select Menu add karne ke liye |

---

## ðŸ§¾ Simple Example

```js
const container = new ContainerBuilder()
  .setAccentColor(0x5865F2)
  .addTextDisplayComponents(
    new TextDisplayBuilder().setContent("# Welcome!\n**Click below**")
  )
  .addActionRowComponents(
    new ActionRowBuilder().addComponents(
      new ButtonBuilder()
        .setCustomId("hello")
        .setLabel("Say Hi")
        .setStyle(ButtonStyle.Primary)
    )
  );
```

---

## ðŸ§  Button Click Handling

```js
client.on('interactionCreate', async i => {
  if (!i.isButton()) return;

  if (i.customId === 'hello') {
    await i.reply({ content: "Hi ðŸ‘‹!", ephemeral: true });
  }
});
```

---

## ðŸŽ¨ Visual Layout Example (Dashboard Style)

```js
const dashboard = new ContainerBuilder()
  .setAccentColor(0x2F3136)
  .addTextDisplayComponents(
    new TextDisplayBuilder().setContent("# Server Stats")
  )
  .addSeparatorComponents(
    new SeparatorBuilder().setSpacing(SeparatorSpacingSize.Small)
  )
  .addSectionComponents(
    new SectionBuilder()
      .addTextDisplayComponents(
        new TextDisplayBuilder().setContent("**Online Members**: 1,234"),
        new TextDisplayBuilder().setContent("**Messages Today**: 5,678")
      )
      .setButtonAccessory(
        new ButtonBuilder()
          .setCustomId("refresh_stats")
          .setLabel("Refresh")
          .setStyle(ButtonStyle.Secondary)
      )
  );
```

---

## ðŸ–¼ï¸ Show Images (Product Preview)

```js
new MediaGalleryBuilder()
  .addItems(
    new MediaGalleryItemBuilder()
      .setURL("https://example.com/image1.png")
      .setDescription("Main Image"),
    new MediaGalleryItemBuilder()
      .setURL("https://example.com/image2.png")
      .setDescription("Side View")
  );
```

---

## ðŸ” Migrating from Embeds

| Old Embed Function     | New Component             |
|------------------------|---------------------------|
| `setTitle()`           | `TextDisplayBuilder` with `# Heading` |
| `setDescription()`     | `TextDisplayBuilder`       |
| `addFields()`          | `SectionBuilder` with 1â€“3 text displays |
| `setImage()`           | `MediaGalleryBuilder`      |
| `setThumbnail()`       | `SectionBuilder.setThumbnailAccessory()` |
| `setColor()`           | `ContainerBuilder.setAccentColor()` |

---

## âš ï¸ Important Tips

- âœ… **Always set this flag** in message: `MessageFlags.IsComponentsV2`
- ðŸ”¢ Max 40 components per message (container + inside elements)
- ðŸ“± Test layouts on mobile too
- ðŸª„ Use `SeparatorBuilder` for spacing or visual breaks
- ðŸ§¼ Keep layout simple, clean, and organized

---

## ðŸ§ª Example with Interactions + Flags

```js
await interaction.reply({
  components: [container],
  flags: [MessageFlags.IsComponentsV2]
});
```

---

## ðŸ“¦ Advanced Tips

### Pagination Example:

```js
class PaginatedContainer {
  constructor(data, pageSize = 5) {
    this.data = data;
    this.pageSize = pageSize;
    this.page = 0;
  }

  buildPage() {
    const start = this.page * this.pageSize;
    const items = this.data.slice(start, start + this.pageSize);

    const container = new ContainerBuilder()
      .addTextDisplayComponents(
        new TextDisplayBuilder().setContent(`# Page ${this.page + 1}`)
      );

    items.forEach(item => {
      container.addSectionComponents(
        new SectionBuilder().addTextDisplayComponents(
          new TextDisplayBuilder().setContent(`**${item.title}**\n${item.desc}`)
        )
      );
    });

    const buttons = [];

    if (this.page > 0) {
      buttons.push(
        new ButtonBuilder().setCustomId("prev_page").setLabel("Prev").setStyle(ButtonStyle.Secondary)
      );
    }

    if ((this.page + 1) * this.pageSize < this.data.length) {
      buttons.push(
        new ButtonBuilder().setCustomId("next_page").setLabel("Next").setStyle(ButtonStyle.Secondary)
      );
    }

    if (buttons.length) {
      container.addActionRowComponents(
        new ActionRowBuilder().addComponents(...buttons)
      );
    }

    return container;
  }
}
```

---

## ðŸ Conclusion

Components v2 is not just an update â€” it's a **new way of building Discord messages**.

> Socho layout ke hisab se. Message ko design karo block by block. Aur practice se expert ban jaoge.

Start basic. Use 1â€“2 components. Dekho kaise dikh raha hai. Fir gradually sections, galleries, spacing, actions sab add karo.

---

ðŸ‘·â€â™‚ï¸ Bana rahe ho ek modern UI for Discord? **Components v2 is your new best friend.**

Need help or want example files? Just ask.  
Happy Building! ðŸ’»âœ¨
