# Step-by-step Item Debugging


# Picking a Version

As of game versions `1.16.100` and onward, there are three distinct types of items, as constituted by its `format_version`. 
In short, versions `1.16.0` and prior are currently the stable (This includes **1.16, 1.14, 1.13, 1.12**) **non-experimental** version. These do not require `Holiday Creator Features` to be enabled. 
	Versions `1.16.100` or over are **experimental**. These items **will not work** unless `Holiday Creator Features` is enabled in the world. Before troubleshooting, please ensure that you have in mind a format that you'd want to use for your item.

## Version Dependent Components
Among the three main Item Versions, there are also different sets of item components. **It is absolutely imperative that the correct components and syntax are used for their respective versions**. A failure to meet such criteria will always result in a broken item.

# All Items

## 1.0 - Pack Updating/Presence
Are the packs *both* active in your world of testing? (You may check this by going to world settings > behavior/resource packs) Further, are they both set up to properly update? That is, are you either using **development folders** or creating a **new world** each pack update? Ensuring that the packs are actually changing per pack-update is always first step in troubleshooting.

## 1.5 - Determining Pack [Resource or Behavior]
Determining which pack the error is actually in is also very important. There are a few surefire ways to prove which it is in (if not both): 
*-If the item is invisible, often constantly throwing the error,  `[Item] requires either an icon atlas or icon texture`, the error is in the `resource pack`. 
	-If the item is showing the black-magenta checkerboard texture, or the "missing" texture, the error is contained in the `resource pack`.
	-If the item fails to register at all, that is, not showing in the inventory or through commands, the error is in the `behavior pack`*.

## 2.0 - Fixing Behaviors
If the item fails to register at all, that is, not showing in the inventory or through commands, the error is in the `behavior pack`. To fix this, there are a few big things to consider:

- Is the `.json` syntax valid? A validator can be found here: https://jsonlint.com/

- What does the content log say? Always consider what the log is outputting. 

- Is the pack enabled in the world? (it happens to the best of us)

- *Make sure that all component names match those found in documentation. Remember*: **no spaces or capitals**

## 3.0 - Fixing Resources
If the item is showing the black-magenta checkerboard texture, or constantly throwing the error,  `[Item] requires either an icon atlas or icon texture`, the error is in the `resource pack`. There are a few universal things to consider here, too:

- Are your texture paths correct? These are the folders that all lead to your texture file, as defined in `resourcepack\textures\item_texture.json`. For example:

```json
{
	"texture_name":  "atlas.items",
	"resource_pack_name":  "vanilla",
		"texture_data": {
			"amethyst_sword": {
				"textures": "textures/items/amethyst_sword"
		}
	}
}
```
*This texture should be in the folder `"textures/items/"`, and the image should be called `amethyst_sword.png`.*

- Does your `"minecraft:icon"` component(behavior or resource, same concept here) point toward the correct short name?

```json
{
	"minecraft:icon": "amethyst_sword"
},
```
