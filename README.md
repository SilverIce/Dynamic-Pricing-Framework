# Dynamic Pricing Framework

## Price range compression

Rules may use `priceRangeCompression` to reduce the effect of every other price
modifier while preserving the item's base value as the fixed point:

```text
compressed price = base price + (calculated price - base price) * compression
```

The framework first calculates the price normally, including Dynamic Pricing
Framework rules and Skyrim's barter multipliers, then applies the compression.
`0.0` always returns the base value, `1.0` preserves the calculated price, and
values between them compress the price range toward the base value.

```json
[
  {
    "description": "Reduce the effect of barter perks for selected items.",
    "itemKeyword": "MyPriceControlledItem",
    "priceRangeCompression": 0.5
  }
]
```

For an item with a base value of `100`, a normally calculated price of `400`
becomes `250`. A normally calculated price of `50` becomes `75`.

If several matching rules specify `priceRangeCompression`, their values are
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
