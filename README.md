# LKB-Configurator Keyboard Configs

键盘配置文件目录。

## 键盘配置添加指南

0. Fork 本仓库
1. 查看下面的数据结构内容，然后参考现有的配置文件，编写你的配置文件。
  - 相同厂商的VID应当保持一致，同时不同厂商的VID应当不重复
  - 不同产品的VID和PID组合应当不一致
2. 将你的配置文件放在对应厂商的文件夹下
3. 编辑`index.ts`文件，将你的配置文件添加到内部
  - 新的厂商应当放在现有配置文件的最后
  - 请勿修改其他厂商的配置文件顺序
4. 向本仓库发起 Pull Request

## 添加要求

非商业授权：

1. 软硬件必须完全开源，并指明特定的许可证。对于硬件，必须在 Github 上给出硬件原始工程文件（而不仅仅是生产文件）；对于软件，必须在 Github 上给出能够正常编译的源代码。
2. 不可以在此过程中获取任何的金钱上的收益，包括但不限于通过任何渠道的售卖、团购、代工等。

商业授权：

1. 请通过邮件联系后再行添加。

## 数据结构

```typescript

export class KeyboardVendor {
    Name!: string;
    Url!: string;
}

/**
 * 键盘Profile
 */
export class KeyboardProfile {
    /**
     * 键盘名称
     */
    Name!: string;

    /**
     * 制造商
     */
    Vendor!: KeyboardVendor;

    /**
     * 对应VID
     */
    VID!: number;

    /**
     * 对应PID
     */
    PID!: number;

    /**
     * 硬件版本号
     */
    Revision!: string[];

    /**
     * 是否是隐藏的配置文件
     */
    Hidden?: boolean;

    /**
     * 额外的设置项目
     */
    AdditionSettings?: KeyboardSetting[];

    /**
     * 额外的Fn项目
     */
    AdditionFns?: Fn[];

    /**
     * 键盘布局
     */
    Layout!: LayoutExt;

    /**
     * 按键阵列行数
     */
    Row!: number;

    /**
     * 按键阵列列数
     */
    Col!: number;

    /**
     * 额外文档说明
     */
    Doc!: string;

    /**
     * 默认配置数据
     */
    Default?: ConfiguratorData;
}

/**
 * 可配置项目
 */
export class KeyboardSetting {
    /**
     * 配置项目的ID
     */
    ID!: number;
    /**
     * 配置数据长度(Byte)
     */
    Length!: number;
    /**
     * 默认值
     */
    DefaultVal!: number;
    /**
     * 配置名称
     */
    Name!: string | StringI18N;
    /**
     * 描述
     */
    Desc?: string | StringI18N;
    /**
     * 选择范围
     */
    Range!: KeyboardSettingNumber | KeyboardSettingDropdown;
}

/**
 * 数值类型的项目值
 */
export class KeyboardSettingNumber {
    /**
     * 最小值
     */
    MinVal!: number;
    /**
     * 最大值
     */
    MaxVal!: number;
    /**
     * 单位
     */
    Unit!: string | StringI18N;
}

export class KeyboardSettingDropdownItem {
    /**
     * 值
     */
    Key!: number;

    /**
     * 条目名称
     */
    Name!: string | StringI18N;
}

export class LayoutCondition {
    id!: string;
    desc?: string | StringI18N;
    cond!: (string | StringI18N)[];
    value!: number;
}

export class LayoutKeyCondition {
    id!: string;
    value!: number;
}

export class LayoutKeyExt extends LayoutKey {
    cond?: LayoutKeyCondition;
    conds?: LayoutKeyCondition[];
}

export class LayoutRowExt {
    keys: LayoutKeyExt[] = [];
}

export class LayoutExt {
    rows: LayoutRowExt[] = [];
    conds: LayoutCondition[] = [];
}

export class Fn {
    id!: number;
    opt!: number;
    desc!: KeyDescription;
    /**
     * 是否是隐藏的功能键
     */
    hide?: boolean;
}

export class KeyDescription {
    upper!: string | StringI18N;
    lower?: string | StringI18N;
    remarks?: string | StringI18N;
    alt?: string;
}

export class StringI18N {
    [key: string]: string;
}

```
