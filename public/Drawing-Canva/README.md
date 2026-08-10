# Drawing Canvas App

A full-featured web-based drawing application with multiple tools, undo/redo functionality, and real-time shape previewing for creating digital artwork directly in your browser.

## Description

Drawing Canvas App (Drawing-Canva) is an intuitive digital drawing tool that brings the power of professional drawing software to your web browser. Create freehand drawings, precise geometric shapes, and pixel-perfect artwork using a variety of tools. Undo mistakes instantly, preview shapes before committing, and export your masterpiece as a PNG image. Perfect for digital artists, designers, and anyone who wants to sketch quickly without installing software.

## Features

- **Drawing Tools**:
  - **Brush**: Freehand drawing with adjustable size and color
  - **Eraser**: Remove content with canvas background color
  - **Line**: Draw straight lines between two points
  - **Rectangle**: Create outlined rectangles with live preview
  - **Circle**: Draw circles with dynamic radius preview
  - **Color Picker**: Sample colors directly from the canvas
- **Brush Controls**:
  - **Adjustable Brush Size**: 1 to 50 pixels with real-time preview
  - **Primary Color Picker**: Choose any color for drawing
  - **Canvas Background**: Set canvas background color
- **Canvas Operations**:
  - **Fill Canvas**: Quickly fill entire canvas with primary color
  - **Clear Canvas**: Erase all content and return to blank canvas
  - **Undo/Redo**: Up to 30 states with full undo/redo support
- **File Management**:
  - **Download Drawing**: Export canvas as PNG image file
  - **Open Image**: Load existing images onto canvas for editing
  - **Automatic Image Scaling**: Imported images scale to fit canvas
- **Keyboard Shortcuts**:
  - **Ctrl + Z**: Undo last action
  - **Ctrl + Y**: Redo last undone action
  - **Ctrl + S**: Download current drawing
- **Live Feedback**:
  - **Current Tool Display**: Shows active tool in top bar
  - **Mouse Position Tracker**: Real-time X/Y coordinates
  - **Canvas Size Display**: Shows current canvas dimensions
  - **Shape Preview**: See shapes before finalizing (line, rectangle, circle)
- **Responsive Design**: Canvas scales with window resize while preserving drawing
- **Active Tool Highlighting**: Visual indicator of currently selected tool
- **Professional UI**: Clean, organized left toolbar with grouped controls
- **No Dependencies**: Pure vanilla JavaScript with HTML5 Canvas API

## Tech Stack

- **HTML5** — semantic structure, Canvas element, file input
- **CSS3** — flexbox layout, custom properties (variables), smooth transitions, styling
- **Vanilla JavaScript (ES6)** — Canvas 2D API, event handling, state management (undo/redo stacks), file I/O

## Folder Structure

```text
Drawing-Canva/
│
├── index.html      # App structure — toolbar, canvas, controls
├── index.js         # Drawing logic, tool handlers, undo/redo management
├── style.css        # Layout, colors, component styling
└── README.md        # Project documentation
```

## Setup / Run Instructions

No build step or dependencies required. Canvas drawing is built into modern browsers.

### Option 1: Open Directly
1. Navigate to the `Drawing-Canva` folder.
2. Double-click `index.html` to open in your browser.

### Option 2: Use a Local Server (recommended)
Using VS Code:
1. Install the **Live Server** extension.
2. Open the project folder in VS Code.
3. Right-click `index.html` → **Open with Live Server**.

> **Note**: Some features (like opening local images) work better with a local server due to browser security restrictions.

## Usage

### Selecting Tools

**Method 1: Click Tool Button**
- In the left toolbar, click any tool icon
- Active tool highlights in blue
- Top bar displays current tool name

**Method 2: Tool Icons** (left toolbar, "Tools" section)
- 🎨 **Brush** (paintbrush icon) — freehand drawing
- 🧹 **Eraser** (eraser icon) — remove content
- ➖ **Line** (minus icon) — straight lines
- ▭ **Rectangle** (square icon) — outlined rectangles
- ◯ **Circle** (circle icon) — outlined circles
- 🎯 **Color Picker** (eyedropper icon) — sample colors

### Drawing with Brush & Eraser

1. Select **Brush** or **Eraser** from tools
2. Click and drag on canvas to draw
3. Release mouse to stop drawing
4. Adjust brush size via slider before or during drawing
5. Change color with color picker (Brush only)

### Drawing Shapes

**Lines**:
1. Select **Line** tool
2. Click starting point on canvas
3. Drag to ending point
4. See live preview as you drag
5. Release to finalize

**Rectangles**:
1. Select **Rectangle** tool
2. Click top-left corner
3. Drag to bottom-right corner
4. See outline preview in real-time
5. Release to complete

**Circles**:
1. Select **Circle** tool
2. Click center point
3. Drag outward to set radius
4. See circle preview as you drag
5. Release to finalize

### Adjusting Brush Size

1. Find **Brush Size** slider in left panel
2. Drag slider left (smaller) or right (larger): 1-50 pixels
3. Size value updates in real-time next to label
4. Changes apply immediately to current and future strokes

### Changing Colors

**Primary Color (Drawing)**:
1. Click the **Primary Color** color picker
2. Choose color from palette or enter hex code
3. Click OK to confirm
4. All new strokes use selected color

**Canvas Background**:
1. Click the **Canvas Background** color picker
2. Select desired background color
3. Eraser will use this background color
4. Changes apply without affecting existing drawing

### Canvas Operations

**Fill Canvas**:
- Click **Fill Canvas** button
- Entire canvas fills with primary color instantly
- Action can be undone

**Clear Canvas**:
- Click **Clear Canvas** button
- All drawing erased, returns to background color
- You'll be asked to confirm before clearing

### Undo & Redo

**Undo Last Action**:
- Click **Undo** button, OR
- Press **Ctrl + Z**, OR
- Multiple clicks undo multiple actions (up to 30 states)

**Redo Last Undone Action**:
- Click **Redo** button, OR
- Press **Ctrl + Y**, OR
- Undo a redo with Undo again

> Note: Redo stack clears when you perform a new action after undoing

### Working with Images

**Open/Load Image**:
1. Click **Open Image** button
2. Select image file from your computer (PNG, JPG, GIF, etc.)
3. Image loads and scales to fit canvas
4. Centered automatically
5. Can draw on top of loaded image

**Download Drawing**:
1. Click **Download** button, OR
2. Press **Ctrl + S**
3. Canvas exports as PNG image file
4. Browser downloads `drawing.png` automatically

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| Ctrl + Z | Undo |
| Ctrl + Y | Redo |
| Ctrl + S | Download drawing |

### Live Information

**Top Bar** (shows while drawing):
- **Current Tool**: Name of active tool
- **Mouse Position**: X, Y coordinates relative to canvas

**Status Bar** (bottom):
- **Canvas Size**: Width × Height in pixels
- **Zoom**: Display scale (always 100% in this version)

## How It Works

### Canvas Initialization

```javascript
function initCanvas() {
    canvas.width = canvas.parentElement.clientWidth;
    canvas.height = canvas.parentElement.clientHeight - 80;
    ctx.fillStyle = bgColorPicker.value;
    ctx.fillRect(0, 0, canvas.width, canvas.height);
}
```

Canvas is sized to fill available space, accounting for toolbar and status bar.

### Drawing Tools

**Brush & Eraser**:
- `mousedown`: Begin path at clicked position
- `mousemove`: Draw line to current position continuously
- `mouseup`: End drawing and save state

**Shapes (Line, Rectangle, Circle)**:
- `mousedown`: Save snapshot of current canvas state
- `mousemove`: Restore snapshot and redraw shape live (preview)
- `mouseup`: Finalize and save state

### Undo/Redo System

**State Stacks**:
- `undoStack`: Stores up to 30 canvas states (using ImageData)
- `redoStack`: Temporary stack for redo operations

```javascript
// Save state after each action
undoStack.push(ctx.getImageData(0, 0, canvas.width, canvas.height));

// Undo: pop from undo, push to redo
redoStack.push(undoStack.pop());
ctx.putImageData(undoStack[undoStack.length - 1], 0, 0);
```

### Color Picking

```javascript
function pickColor(e) {
    const pos = getMousePos(e);
    const pixel = ctx.getImageData(pos.x, pos.y, 1, 1).data;
    // Convert RGBA to hex color
    const hex = "#" + ...;
    colorPicker.value = hex;
    setActiveTool("brush", "Brush");
}
```

Samples individual pixel, converts RGBA values to hex, updates color picker, switches to brush.

### Image Loading

```javascript
reader.onload = (event) => {
    const img = new Image();
    img.onload = () => {
        // Calculate scale to fit canvas
        let scale = Math.min(canvas.width / img.width, canvas.height / img.height);
        // Center image
        let x = (canvas.width / 2) - (img.width / 2) * scale;
        let y = (canvas.height / 2) - (img.height / 2) * scale;
        ctx.drawImage(img, x, y, img.width * scale, img.height * scale);
    };
};
```

Scales images proportionally and centers them on canvas.

### Window Resize Handling

```javascript
window.addEventListener("resize", () => {
    const tempImg = ctx.getImageData(0, 0, canvas.width, canvas.height);
    canvas.width = canvas.parentElement.clientWidth;
    canvas.height = canvas.parentElement.clientHeight - 80;
    ctx.putImageData(tempImg, 0, 0);
});
```

Saves drawing before resizing, then restores it with new dimensions.

## Implementation Notes

- **Canvas Coordinate System**: Uses `getBoundingClientRect()` for accurate mouse-to-canvas coordinate conversion accounting for DPI scaling
- **ImageData API**: Undo/Redo uses raw pixel data snapshots for complete state preservation
- **Line Rendering**: `lineCap: "round"` and `lineJoin: "round"` for smooth, professional appearance
- **Shape Preview**: Snapshots enable real-time preview without permanent changes until release
- **Active Tool**: Visual feedback via `active` class on currently selected tool button
- **Color Swatch**: Custom styled color input with proper border-radius for polished look
- **Responsive Toolbar**: Left panel scrolls if content exceeds viewport height

## Educational Value

This project demonstrates:

- HTML5 Canvas 2D API and drawing context
- Canvas coordinate transformation and mouse position tracking
- ImageData manipulation for undo/redo functionality
- File input handling and FileReader API
- Image scaling and centering algorithms
- State management with stacks (undo/redo pattern)
- Event handling (mouse, keyboard, file input)
- Event delegation for tool selection
- DOM manipulation and class toggling
- Responsive design with window resize handling
- Export to image format via `canvas.toDataURL()`
- Performance considerations for frequent canvas operations

## Common Drawing Scenarios

**Quick Sketch**:
1. Select Brush
2. Adjust size if needed
3. Draw freely
4. Download when done

**Precise Diagram**:
1. Use Rectangle and Circle tools for shapes
2. Use Line tool for connections
3. Zoom by resizing window
4. Color picker for exact color matching

**Photo Annotation**:
1. Open Image with existing photo
2. Select Brush
3. Draw annotations on top
4. Download annotated version

**Design Mockup**:
1. Draw rectangles for layout
2. Add lines for divisions
3. Use color picker to match colors
4. Undo and refine as needed

## Keyboard-Only Workflow

1. Tab to tool buttons and press Enter to select
2. Tab to brush size slider and use arrow keys
3. Click canvas to draw
4. Use Ctrl+Z/Ctrl+Y for undo/redo
5. Use Ctrl+S to download

## Performance Notes

- **Undo Stack Limit**: Maximum 30 states to prevent excessive memory usage
- **ImageData Operations**: Heavy operations; noticeable for very large canvases
- **Real-Time Preview**: Shape preview uses efficient snapshot/restore pattern

## Future Enhancements

Potential improvements:

- **Selection Tool**: Select, move, and transform drawn content
- **Text Tool**: Add text annotations with font controls
- **Fill Bucket**: Flood fill tool for areas
- **Layers**: Multiple drawing layers with visibility control
- **Gradient Tool**: Linear and radial gradients
- **Transform Tools**: Rotate, scale, flip drawings
- **Brush Patterns**: Patterns and textures for brush
- **Zoom Controls**: Zoom in/out for detailed work
- **Pan Tool**: Move canvas view around
- **Export Options**: Save as JPG, WebP, SVG
- **Dark Theme**: Dark mode option
- **Touch Support**: Touch events for drawing on tablets
- **Autosave**: Save drawing to localStorage automatically
- **Color Palette**: Saved color swatches for quick access
- **Stroke Smoothing**: Bezier curves for smoother lines
- **Tablet Pressure**: Support for pressure-sensitive tablets

## Browser Compatibility

Works on all modern browsers supporting:
- HTML5 Canvas 2D Context
- ES6 JavaScript
- FileReader API
- Canvas ImageData API

**Tested on**: Chrome, Firefox, Safari, Edge

**Not supported**: IE11 and older

## Accessibility

- Keyboard shortcuts for common actions
- Clear active tool indication
- Semantic HTML structure
- Font Awesome icons with fallback text
- Color contrast meets standards

## License

This project is open-source and available for educational and personal use.

## Author

Contributed as part of the [100 Days 100 Web Projects](../../README.md) challenge.
