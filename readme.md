# AgentTorch Simulation Visualizations

This module provides a Python API to visualize simulations built with **AgentTorch**. It currently supports **GeoPlot** visualization and is designed to be extendable for additional types.

---

## ✨ Supported Visualizations

- **GeoPlot**: Renders a 3D geospatial plot using [CesiumJS](https://cesium.com/cesiumjs/), allowing you to visualize the evolution of agent properties over time.

---

## 📍 GeoPlot

`GeoPlot` renders a CesiumJS-based 3D plot using the state trajectory from your simulation.

It generates:
- A `.html` file that opens in a browser with an interactive Cesium visualization.
- A `.geojson` file containing the plotted data.

### ✅ Example Usage

```python
from agent_torch.visualize import GeoPlot

# Step 1: Create your simulation and runner
# (Assume runner is already set up and configured)

# Step 2: Initialize the visualizer
geoplot = GeoPlot(
    config,
    options={
        "cesium_token": "<Your_Cesium_Ion_Token>",
        "step_time": 3600,  # Optional: Time between steps in seconds
        "coordinates": "consumers/coordinates",
        "feature": "consumers/money_spent",
        "visualization_type": "color"  # or "size"
    }
)

# Step 3: Run simulation and generate visualizations
for i in range(num_episodes):
    runner.step(num_steps_per_episode)
    geoplot.render(
        name=f"consumer-money-spent-{i}",
        state_trajectory=runner.state_trajectory
    )
```

## ⚙️ GeoPlot Options

| Option               | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| `cesium_token`       | Your [Cesium Ion access token](https://cesium.com/ion/)                     |
| `step_time`          | Time between each step in seconds (e.g., `3600` for 1 hour)                 |
| `coordinates`        | Path to agent position in the state (e.g., `consumers/coordinates`)         |
| `feature`            | Path to the property to visualize (e.g., `consumers/money_spent`)           |
| `visualization_type` | `'color'` or `'size'` – controls how property values are visually rendered  |

---

## 📦 Output Files

After calling `render()`, the following files will be generated:

- `consumer-money-spent-{episode}.html`:  
  Opens in a browser to show an interactive 3D map with plotted agent data.

- `consumer-money-spent-{episode}.geojson`:  
  Contains raw geospatial and feature data used in the visualization.

---

## 💡 Contributing

We welcome contributions! 🎉

To request a new visualization type, suggest improvements, or report issues:

- [Open an issue](https://github.com/your-repo/issues)
- Submit a [pull request](https://github.com/your-repo/pulls)

Please follow standard contribution guidelines and ensure your code is well-documented and tested.

---
