
# 🪄 MagicSpells Skript — Complete Wiki

*A full-featured spell engine built in Skript (no external MagicSpells plugin required).*

---

## 📦 Overview

A complete Skript-based magic system with mana, cooldowns, particles, GUI and customizable spells compatible with all Minecraft versions.

It provides:
- Custom mana system
- Configurable spells
- Particles & sounds
- Cooldowns & item costs
- GUI menu (`/spells`)
- Custom event API
- Cross-version support (1.8 → 1.21+)

---

## ⚙️ Requirements

| Plugin | Purpose |
|:-------|:---------|
| **Skript** | Core scripting plugin |
| **SkBee** | Particles, action bars |
| **SkQuery / Skellett** | Additional effects & events |
| **TuSKe** *(optional)* | GUI handling |
| **skript-mirror** *(optional)* | Java reflection for future API features |

✅ Works fine even with only **Skript + SkBee + SkQuery**.

---

## 📁 File Structure

```
/plugins/Skript/scripts/
├── MagicSpells.sk        ← Main engine
└── Spells_Example.sk     ← Example spell pack
```

---

## 💬 Commands

| Command | Permission | Description |
|:---------|:-------------|:-------------|
| `/cast <spell>` | `magicspells.cast` | Cast a spell directly by name |
| `/spells [page]` | none | Open spell GUI |
| `/mana` | none | View mana |
| `/msreload` | `magicspells.reload` | Reload MagicSpells scripts |

---

## 🧙‍♂️ Example Spells (Included)

| Name | Type | Cost | Cooldown | Description |
|:------|:------|:------|:-----------|:-------------|
| Fireball | fireball | 20 | 6s | Launch a small fireball |
| Explode | aoe | 40 | 20s | Create a magic explosion |
| Lightning | lightning | 30 | 15s | Summon lightning |
| ArcaneArrow | projectile | 8 | 3s | Fire an arcane arrow |
| Heal / MassHeal | heal | 15 / 40 | 8 / 40s | Restore HP |
| Blink / Phase | tp | 10 / 25 | 5 / 20s | Teleport forward |
| Shield / Rage / Haste | buff | Varies | Varies | Temporary effects |
| Meteor / Apocalypse | custom / aoe | 60 / 120 | 60 / 300s | Ultimate attacks |
| Light / Detect | custom | 5 / 4 | 2 / 5s | Utility spells |

---

## 🔮 Mana System

Players start with configurable mana, which regenerates automatically every few seconds.

Edit these values in `MagicSpells.sk`:

```skript
options:
  mana-max: 100
  mana-start: 100
  mana-regen: 2
  mana-regen-interval: 2 seconds
```

Displayed every 2s via action bar:  
`&bMana: &e80 / 100`

---

## 🪙 Costs & Cooldowns

Each spell supports mana, cooldown, and optional item costs.

```skript
ms-register("Meteor", "custom", 60, 60, "magic.meteor", "DIAMOND:3", 6, "&4A meteor crashes down!", "Ultimate")
```

---

## 🎇 Particle & Sound Effects

Each spell includes visual feedback (particles, sounds).  
You can use provided particle helpers:

```skript
drawCircleLoc(location, radius, "flame", 20)
drawSpiral(player, 2, "heart", 3, 20)
drawLineLoc(start, end, "portal", 30)
```

---

## 🧾 Creating Custom Spells

Register new spells in any `.sk` file:

```skript
ms-register("IceBlast", "aoe", 25, 8, "magic.iceblast", "SNOWBALL:3", 4, "&bYou unleash a freezing blast!", "Offensive")
```

| Parameter | Example | Description |
|:-----------|:-----------|:-------------|
| name | "Fireball" | Display name |
| type | "fireball" | Spell behavior |
| manaCost | 20 | Mana cost |
| cooldown | 6 | Cooldown (s) |
| permission | "magic.fireball" | Required permission |
| itemCostStr | "DIAMOND:3" | Optional item cost |
| power | 1.2 | Spell intensity |
| message | "&aSpell cast!" | Feedback |
| category | "Offensive" | GUI category |

---

## ⚡ Spell Types

| Type | Description |
|:------|:-------------|
| fireball | Launches a small fireball |
| projectile | Shoots an arrow |
| heal | Restores health |
| tp | Teleports the player |
| lightning | Summons a lightning bolt |
| speed | Gives Speed effect |
| buff | Gives Strength effect |
| aoe | Area damage |
| custom | Triggers MagicSpellsCustomCast event |

---

## 🧩 Custom Event API

```skript
on custom event "MagicSpellsCustomCast":
    if {_ms.lastcast.%uuid of player%} is set:
        set {_spell} to {_ms.lastcast.%uuid of player%}
        if {_spell} = "tornado":
            loop all entities in radius 6 around location of player:
                if loop-entity is a living entity and loop-entity is not player:
                    push loop-entity upwards by 1.2
            send "&9Tornado tosses enemies!" to player
```

---

## 🧰 Developer API

| Function | Returns | Description |
|:-----------|:-----------|:-------------|
| `ms-register()` | none | Register new spell |
| `ms-getmana(player)` | number | Get mana |
| `ms-takemana(player, amount)` | boolean | Deduct mana |
| `ms-addmana(player, amount)` | none | Add mana |
| `ms-set-cooldown(player, spell, seconds)` | none | Apply cooldown |
| `ms-on-cooldown(player, spell)` | boolean | Check cooldown |

---

## 🔐 Permissions

| Permission | Description |
|:-------------|:-------------|
| `magicspells.cast` | Allow /cast and GUI use |
| `magicspells.reload` | Reload scripts |
| `magic.<spell>` | Per-spell permission |

---

## 🚀 Updating & Reloading

```
/sk reload MagicSpells
/sk reload Spells_Example
```
or simply:
```
/msreload
```

---

## 🧩 Compatibility

✅ Works on 1.8 → 1.21+  
✅ Skript 2.6+  
✅ Paper, Spigot, Purpur

---

## 🧠 Troubleshooting

| Issue | Cause | Fix |
|:------|:--------|:----|
| `Unknown particle type` | Particle not in your version | Use a supported particle |
| `Variable not found` | Missing init | Reload or restart |
| `/spells` empty | Spells not registered | Check `ms-register` calls |

---

## 📜 Credits

- Skript make by **DEV_PEGASUS**  
