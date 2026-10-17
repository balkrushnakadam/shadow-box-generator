# 🔦 ShadowBox CAD Studio Pro
**Inverse-Shadow Computational CAD Generator & Real-Time 3D Optical Ray-Tracing Bench**

ShadowBox CAD Studio Pro is a zero-dependency, browser-based CAD application that transforms any 2D silhouette image (`SVG`, `PNG`, `JPG`) into a physical **3D Shadow Projection Box**[span_1](start_span)[span_1](end_span). When a single point-light LED is placed at the center pole of the box, the 4 surrounding walls cast an exact, undistorted 2D silhouette onto the surrounding wall.

---

## ✨ Key Engineering Features

* **Sub-Pixel Bilinear Marching Squares + RDP Simplification:** Extracts ultra-smooth iso-contours from any raster or vector image with zero pixel stair-stepping, followed by Ramer-Douglas-Peucker simplification and shrink-free Taubin spline smoothing[span_2](start_span)[span_2](end_span).
* **True Mitered Conical 3D Extrusion (Zero Optical Parallax):** Unlike standard flat extrusions that clip angled light rays, every vertex on the outer wall face is projected radially along the exact mathematical ray vector from the point light `(0, 0, Z_L)` while miter-welding at `45°` along all four box corners[span_3](start_span)[span_3](end_span).
* **Automatic Floating Island Bridging:** Automatically detects disconnected "floating" shadow pieces (like a crescent moon or floating ornaments) and generates structural bridge struts to anchor them to the main body[span_4](start_span)[span_4](end_span)[span_5](start_span)[span_5](end_span).
* **Dual STL Export Modes:**
  * **Assembled 3D Box (`.STL`):** Ready for 3D optical shadow verification or direct printing.
  * **Flat-Lay 5-Piece Kit (`.STL` - Support-Free!):** Unfolds the 4 conical walls flat onto the print bed around a stepped self-aligning baseplate so the entire lamp prints with **zero overhangs and zero supports**.
* **1:1 Bezier Cardboard / Laser Template (`.SVG`):** Exports a true-scale vector template with Quadratic Bezier curves, glue tabs, a roll-up center pole strip, and a 1:1 pole height gauge[span_6](start_span)[span_6](end_span).
* **Standalone 3D STL Optical Shadow Bench:** Includes a dedicated testing tool (`shadowbox_test_tool.html`) that loads any exported `.STL` file and runs both real-time GPU shadow mapping and an exact CPU triangle ray-tracer to verify shadow accuracy before printing[span_7](start_span)[span_7](end_span).

---

## 🚀 Quick-Start Workflow

1. **Load Your Artwork:** Click **📂 Open SVG / PNG / JPG Silhouette** (or paste raw `<svg>` XML code)[span_8](start_span)[span_8](end_span). High-contrast black-and-white silhouettes work best[span_9](start_span)[span_9](end_span).
2. **Frame Your Shadow:** Adjust **Image Zoom (%)** and **Horizontal/Vertical Shift** so your artwork sits nicely around the red center box footprint in the bottom-left mini preview[span_10](start_span)[span_10](end_span).*(Note: The red rectangle represents the physical baseplate footprint on the wall[span_11](start_span)[span_11](end_span).)*
3. **Configure Box & Light Specs:** Set your desired **Inner Box Width/Height** (`W`, `H`), **Shadow Size on Wall** (`S`), and **Point Light Distance** (`Z_L`)[span_12](start_span)[span_12](end_span).
4. **Inspect Live 3D Simulation:** Orbit the 3D viewport to inspect the projected shadow and toggle **Show Error Diff on Wall** to see how closely the physical 3D walls match your target image (`Projected Shadow Match %`)[span_13](start_span)[span_13](end_span).
5. **Export & Build:**
   * Click **🧩 Download Flat-Lay 5-Piece Kit (.STL)** for easy, support-free 3D printing.
   * Click **Download Assembled 3D Box (.STL)** to test the 3D mesh in the **🔬 3D STL Shadow Bench & Tester**[span_14](start_span)[span_14](end_span).
   * Click **Download Sub-Pixel Bezier Template (.SVG)** for laser cutting or hand-cutting out of black cardstock/cardboard[span_15](start_span)[span_15](end_span).

---

## 🎛️ Complete Settings Reference Guide

### 1. Image & Sub-Pixel Iso-Contouring
| Setting | What It Does | Recommended Value |
| :--- | :--- | :--- |
| **Floating Islands** | Controls how disconnected shadow regions (not touching the base) are handled:<br>• **Auto-Bridge to Main Body:** Automatically connects floating pieces to the nearest grounded wall with a structural strut[span_16](start_span)[span_16](end_span).<br>• **Keep Unbridged:** Leaves islands floating in mid-air (for optical comparison only)[span_17](start_span)[span_17](end_span).<br>• **Remove Disconnected:** Deletes floating islands that cannot support themselves[span_18](start_span)[span_18](end_span). | `Auto-Bridge to Main Body`[span_19](start_span)[span_19](end_span) |
| **Bridge Strut Width (mm)** | Sets the physical width (in millimeters) of the support struts generated for floating islands[span_20](start_span)[span_20](end_span). | `1.4 mm – 2.0 mm`[span_21](start_span)[span_21](end_span) |
| **Taubin Curve Smoothing Passes** | Applies shrink-free alternating Laplacian smoothing (`+0.42 / -0.40`) to contour loops[span_22](start_span)[span_22](end_span). Higher values make curves silkier; lower values preserve sharp corners and tiny details. | `2 – 3`[span_23](start_span)[span_23](end_span) |
| **Contour Resolution (Sub-Pixel Grid)** | Controls the sampling density of the Marching Squares grid across each wall[span_24](start_span)[span_24](end_span). Higher values capture tiny details (like beads or thin strands) at the cost of a larger STL file. | `480 – 520` for detailed art[span_25](start_span)[span_25](end_span) |
| **Invert B&W** | Swaps black and white regions in your input image (useful if your silhouette is white on a black background)[span_26](start_span)[span_26](end_span). | Unchecked (Default expects Black = Shadow)[span_27](start_span)[span_27](end_span) |
| **Flip Horizontal** | Mirrors the input silhouette left-to-right[span_28](start_span)[span_28](end_span). | Optional[span_29](start_span)[span_29](end_span) |
| **Show Error Diff on Wall** | Overlays a live diagnostic comparison on the 3D wall:<br>• **Cyan:** Extra shadow cast by structural bridges or the base rim[span_30](start_span)[span_30](end_span).<br>• **Magenta/Pink:** Target shadow areas cut off or missing[span_31](start_span)[span_31](end_span). | Use for inspection[span_32](start_span)[span_32](end_span) |
| **Image Zoom (%) & Shift X / Y (mm)** | Scales and translates the projected shadow on the wall relative to the center box footprint[span_33](start_span)[span_33](end_span). | Adjust so key details aren't hidden inside the red box[span_34](start_span)[span_34](end_span) |

---

### 2. Box & Shadow Dimensions
| Setting | What It Does |
| :--- | :--- |
| **Inner Box Width `W` (mm)** | The internal horizontal width of the shadow box (excluding wall thickness `T`)[span_35](start_span)[span_35](end_span). |
| **Inner Box Height `H` (mm)** | The internal vertical height of the shadow box (excluding wall thickness `T`)[span_36](start_span)[span_36](end_span). |
| **Shadow Size on Wall `S` (mm)** | The total width/height of the projected shadow image on the wall when the box is mounted flush against the wall (`Z = 0`)[span_37](start_span)[span_37](end_span). Increasing `S` makes the wall cutouts sit higher up on the box walls; decreasing `S` compresses the cutouts closer to the baseplate. |

---

### 3. Point Light & Conical Wall Geometry
| Setting | What It Does |
| :--- | :--- |
| **Point Light Distance `Z_L` (mm)** | The exact distance from the wall (`Z = 0`) to the glowing center of your LED filament/emitter[span_38](start_span)[span_38](end_span). **Crucial:** For the shadow to project at the exact right scale and alignment, your physical LED must sit at `Z_L`[span_39](start_span)[span_39](end_span)! |
| **LED Bulb Tip Offset (mm)** | The distance from the top of the 3D-printed center stalk to the center of the LED emitter (`Physical Pole Length = Z_L - LED Offset`)[span_40](start_span)[span_40](end_span). For example, if `Z_L = 75 mm` and your LED dome sticks out `6 mm` past the tube, set this to `6 mm` so the printed tube stops at `69 mm`[span_41](start_span)[span_41](end_span). |
| **Pole Outer Diameter (mm)** | Outer diameter of the center hollow tube that holds your LED[span_42](start_span)[span_42](end_span). |
| **Inner Wire Hole Diameter (mm)** | Inner bore diameter through the center pole and baseplate for routing LED power wires[span_43](start_span)[span_43](end_span). |
| **Conical Wall Thickness `T` (mm)** | Physical thickness of the 4 walls and baseplate (`2.0 mm` is ideal for rigid 3D printing)[span_44](start_span)[span_44](end_span). |
| **Glue Tabs in SVG** | Adds fold-and-glue corner tabs to the exported `.SVG` cardboard template[span_45](start_span)[span_45](end_span). |
| **3D Light Cone** | Toggles the yellow perspective guide lines from the LED to the corners of the shadow on the wall[span_46](start_span)[span_46](end_span). |

---

## 🖨️ 3D Printing & Assembly Tips

### Option A: Printing the Flat-Lay 5-Piece Kit (Recommended)
1. Download the **Flat-Lay 5-Piece Kit (`.STL`)** and open it in your slicer (PrusaSlicer, OrcaSlicer, Bambu Studio, Cura).
2. **Supports:** **OFF** (None needed!).
3. **Layer Height:** Use **`0.12 mm` or `0.16 mm`** so the conical ray-angled bevels along the cutout edges are sliced smoothly.
4. **Wall Generator:** Turn on **Arachne** perimeter generation so fine features (like thin prongs or hair strands) print cleanly.
5. **Smaller Print Beds:** Right-click the model in your slicer and select **Split to Objects** to arrange the 5 pieces across smaller build plates.
6. **Assembly:** Fold the 4 walls up `90°` so the **smooth bottom side that touched the print bed faces INWARD toward the LED pole**, and glue them against the raised inner alignment lip on the baseplate.

### Option B: Printing the Assembled 3D Box in One Piece
1. Download the **Assembled 3D Box (`.STL`)**.
2. Enable **Tree Supports (On Build Plate Only)** for overhangs `> 55°` to support internal cutout arches.

### 💡 Choosing the Right LED Light Source
To get razor-sharp shadows on your wall, **do not use a frosted/diffused bulb**. Use a **single-point clear LED** (such as a 3mm/5mm clear high-brightness LED, a tiny SMD LED, or a single-filament G4/COB point emitter) positioned at your exact `Z_L` height!
