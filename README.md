# Dynamic Pricing Framework

## Price multiplier compression

Rules may use `priceMultiplierCompression` to compress the final price
multiplier toward its neutral value of `1.0`:

```text
calculated multiplier = DPF multiplier * Skyrim barter multiplier * other multipliers
compressed multiplier = 1 + (calculated multiplier - 1) * compression
final price = base price * compressed multiplier
```

The framework first calculates the price normally, including Dynamic Pricing
Framework rules and Skyrim's barter multipliers, then applies the compression.
`0.0` produces a neutral multiplier of `1.0`, `1.0` preserves the calculated
multiplier, and values between them reduce the effect of all price modifiers.

```json
[
  {
    "description": "Reduce the effect of barter perks for selected items.",
    "itemKeyword": "MyPriceControlledItem",
    "priceMultiplierCompression": 0.5
  }
]
```

For example, with a base value of `100`, a DPF multiplier of `1.25`, a Skyrim
barter multiplier of `3.2`, and a compression of `0.5`:

```text
calculated multiplier = 1.25 * 3.2 = 4.0
compressed multiplier = 1 + (4.0 - 1) * 0.5 = 2.5
final price = 100 * 2.5 = 250
```

A normally calculated multiplier of `0.5` is compressed to `0.75` by the same
factor, changing a price of `50` to `75` for an item with a base value of `100`.

If several matching rules specify `priceMultiplierCompression`, their values are
multiplied. For example, two matching values of `0.5` produce an effective
compression of `0.25`.

#### YOU NEED CMAKE < 3.5 !

#### WINDOWS ENVIRONMENT VARIABLES TO SET

1. **`COMMONLIB_SSE_FOLDER`**: The path to your clone of Commonlib.
2. **`VCPKG_ROOT`**: The path to your clone of [vcpkg](https://github.com/microsoft/vcpkg).
3. (optional) **`SKYRIM_FOLDER`**: path of your Skyrim Special Edition folder.
4. (optional) **`SKYRIM_MODS_FOLDER`**: path of the folder where your mods are.

#### THINGS TO EDIT

1. CMakeLists.txt
- **`AUTHORNAME`**
- **`MDDNAME`**
- (optional) Your plugin version. Default: `0.1.0.0`
2. vcpkg.json
- **`name`**: Your plugin's name.
- **`version-string`**: Your plugin version. Default: `0.1.0.0`

#### FEATURES
Automatically imports:
- [CLibUtil](https://github.com/powerof3/CLibUtil) by powerof3
- [SKSE Menu Framework](https://www.nexusmods.com/skyrimspecialedition/mods/120352) by Thiago099
