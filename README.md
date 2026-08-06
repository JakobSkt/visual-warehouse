# VisualWarehouse

Everything that you need to organize your warehouse.<br>
Now more engaging and visual than ever
### Demo
https://visual-warehouse.vercel.app/

### Tested devices
The prototype is developed and optimized for the following devices:
* MacBook Pro 14" (1512 x 900px)
* Pixel 8 (412 x 915px)

### Features
* Sorting items in table view
* Dark mode switch through npm module `mode-watcher`
* Keyboard shortcuts through npm module `svelte-keyboard-shortcuts`

#### Keyboard shortcuts
* `h` - Navigates to home page
* `a` - Starting key for the 'Actions'. Press any of the following keys to place items:
  * `t` - Presses 'Truck' button
  * `r` - Presses 'Rack' button
  * `p` - Presses 'Pallet' button
  * `s` - Presses 'Small pallet' button
  * `c` - Presses 'Blue crates' button
  * `w` - Presses 'Plastic wrap' button
  
* `r` - Opens the receive view
  * `c` - Closes the receive panel
* `s` - Opens the ship view
  * `c` - Closes the ship panel

* `m` - Toggles between light and dark mode


### Running the app
* Clone the project  
* Install dependencies with `npm install` (or `pnpm install` or `yarn`).
* Start a development server with:

```sh
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```
