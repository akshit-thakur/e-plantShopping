# 🌿 Paradise Nursery — e-plantShopping

A React + Redux single-page shop for houseplants. Built as the capstone for the Coursera **"Developing Front-End Apps with React"** course (IBM Full-Stack Developer specialization).

## ✨ Features

- Branded landing page with a "Get Started" call-to-action.
- Plant catalog grouped by category (Air Purifying, Aromatic, Insect Repellent, Medicinal, Low Maintenance).
- Each plant card shows image, name, description, price, and an **Add to Cart** button that becomes disabled and labeled **Added to Cart** once clicked.
- Live cart badge in the header reflecting the total quantity of items.
- Cart view with per-item increment/decrement, delete, item subtotal, and overall total — all updated in real time via Redux.
- **Continue Shopping** to return to the catalog and a **Checkout** placeholder action.

## 🛠 Tech Stack

- [React 18](https://react.dev/)
- [Redux Toolkit](https://redux-toolkit.js.org/) + [React-Redux](https://react-redux.js.org/)
- [Vite](https://vitejs.dev/) for dev server and bundling
- ESLint for linting
- `gh-pages` for static deployment

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ and npm

### Install

```bash
npm install
```

### Run the dev server

```bash
npm run dev
```

Then open the URL printed by Vite (typically http://localhost:5173).

### Build for production

```bash
npm run build
```

### Preview the production build

```bash
npm run preview
```

### Lint

```bash
npm run lint
```

## 📁 Project Structure

```
src/
├── App.jsx            # Root component; toggles landing page ↔ product list
├── main.jsx           # React entry point; wires up Redux <Provider>
├── store.js           # Redux store configuration
├── CartSlice.jsx      # Redux slice: addItem / removeItem / updateQuantity
├── ProductList.jsx    # Plant catalog, header, and cart badge
├── CartItem.jsx       # Cart view: quantities, totals, checkout
├── AboutUs.jsx        # About section
└── *.css              # Component styles
```

## 🧠 Redux Overview

State is managed by a single `cart` slice in [src/CartSlice.jsx](src/CartSlice.jsx):

| Action           | Payload                 | Purpose                                           |
| ---------------- | ----------------------- | ------------------------------------------------- |
| `addItem`        | `{ name, image, cost }` | Add a plant to the cart or increment its quantity |
| `removeItem`     | `name`                  | Remove a plant entirely from the cart             |
| `updateQuantity` | `{ name, quantity }`    | Set a plant's quantity to an exact value          |

State shape:

```js
{
  cart: {
    items: [{ name, image, cost, quantity }];
  }
}
```

### How it connects

- **ProductList** dispatches `addItem(plant)` on Add to Cart and reads `state.cart.items` (via `useSelector`) to display the header cart count.
- **CartItem** dispatches `updateQuantity` for the `+` / `-` controls (falling back to `removeItem` when quantity reaches 0) and `removeItem` for Delete. Totals are derived from `state.cart.items` so the UI updates reactively.
- **store.js** wires `cartReducer` into the root reducer; **main.jsx** wraps `<App />` in `<Provider store={store}>`.

## 📦 Deployment

A `gh-pages` dependency is included for GitHub Pages deployment. After configuring the `homepage` field in `package.json`:

```bash
npm run build
npx gh-pages -d dist
```

## 📄 License

See [LICENSE](LICENSE) for details.

## 🙏 Acknowledgements

Scaffold provided by **IBM Developer Skills Network** for the Coursera React course.
