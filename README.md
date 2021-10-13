# Magento Layout Development
- The **basic components** of **page design** are **layouts**, **containers**, and **blocks** in Magento. 
- The **purpose of page layouts** is to create a structured, common set of layout instructions to render pages.
- **Most pages** on a website can be categorized as fitting into a **1,2, or 3-column container system**.
## The Magento page layout
- Layout represents **page structure** using XML file.
- Layouts can be represented by a **hierarchy of elements** that can be represented both as **blocks** and as **containers**. Examples of layouts include the `empty`, `1column`, `2columns-left`, `2columns-right`, and `3columns`.
- **Containers** assign **content structure** to a page using **container tags** within a **layout XML file**. Examples of containers include the `header`, `left column`, `main column`, and `footer`.
- **Blocks** render the **UI elements** on a page using **block tags** within a **layout XML file**. Blocks use templates to generate HTML to insert into its **parent structural block**. Examples of blocks include a `category list`, a `mini cart`, `product tags`, and `product listing`.
### Layout handles
- layout handle is a **uniquely identified set of layout instructions** that serves as a name of a layout file. There are **three kinds** of layout handles. 
- **Page type layout handles**: Corresponds to the **controller name and actions** in its totality. For example, `customer_view`.
- **Page layout handles**: These are used as a **specific pages' identifiers** via parameters. For example, `catalog_product_view_type_simple_id_31`.
- **Arbitrary handles**: Do not correspond to any page type, but other handles use them by including.
## Layout types
- For **each page/template** are available **three types** of **layout files**:
- **Page layout**: The main objective is to set the **page skeleton**. For example, it defines if the rendered layout has **one, two, or three columns** for displaying the content.
- **Page configuration**: Defines the **structure of the page** and which files will be added to render the pages.
- **Generic layout**: Responsible for the **availability and visualization** of the elements in the **body page** in a **detailed manner**.
## Basic layouts
- The **basic view of all Magento storefront pages** is defined in **two page configuration layout files** located in the `Magento_Theme` module:
- `default.xml`: defines the **page layout**.
- `default_head_blocks.xml`: defines the **scripts**, **images**, and **metadata** included in pages’ **head section**.
- These **basic page configuration layouts** are **extended** in other **Magento modules** and in **Magento themes**.
- You can also **extend** and **override** these files in your **custom theme**.
## Layout customizations
- To ensure stability and secure your customizations from being deleted during upgrade, **do not change out-of-the-box Magento module and theme layouts**. To make the necessary changes, **create extending and overriding layout files** in your **custom theme**.
## Layout files processing
- The Magento application processes layout files in the following order:
1. Module **base files** loaded.
2. Module **area files** loaded.
3. Collects **all layout files** from modules. The order is determined by the **modules order** in the **module list** from the `app/etc/config.php` file. (If their priorities are equal, they are sorted according to their **alphabetical priority**.)
4. Determines the **sequence of inherited themes** `[<parent_theme>, …, <parent1_theme>]<current_theme>`
5. **Iterates** the **sequence of themes** from **last ancestor to current**:
     1. **Adds** all **extending theme layout files** to the **list**.
     2. **Replaces** **overridden layout files** in the **list**.
6. **Merges** all layout files from the **list**.
- **Note**: Layout files that belong to **inactive modules** or **modules with disable output** are ignored.
## Layout files validation
- After layouts are merged, magento validates them.
- Layout **validations and error handling** depends on the **application mode** in which your Magento instance runs.
- `Developer mode`: Syntax is validated in `.xml` and `.xsd` files, and `.xml` files are validated according to the **xsd schema**. If any validation fails, the **hard failure** with **process halts** occurs.
- `Production mode or Default mode`: Syntax is validated in `.xml` and `.xsd` files. If validation fails errors are logged to the `var/log` directory without throwing an exception. The validation according to the **xsd schema** is not performed.

