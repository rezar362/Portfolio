# instacart_optimizer_gnn_rl

Real-time delivery route optimization for San Francisco using a Graph Neural Network (GNN) for delay prediction and a Reinforcement Learning (RL) agent for dynamic rerouting — modeled on Instacart-style order patterns.

---

## What it does

- Models SF as a delivery network: 3 warehouses, 15 neighborhoods, real OSM road graph
- Simulates 16,000+ orders over 60 days using Instacart-style demand patterns (peak hours, day-of-week, neighborhood density)
- GNN predicts delivery delay per route based on hour, day, demand, and distance
- RL agent (PPO) dynamically reroutes deliveries when the GNN detects a better option
- Interactive Folium map visualizes delayed vs optimal vs RL-rerouted paths across SF

---

## Results

| Metric | Value |
|---|---|
| GNN Test MAE | ~1.4 min |
| Avg delay before rerouting | 15.94 min |
| Avg delay after rerouting | 13.87 min |
| Improvement per delivery | 2.06 min |
| Reroute rate | 54.6% |
| RL avg reward | 0.0334 |

At 300 deliveries/day, the agent eliminates ~10 hours of cumulative delay daily.

---

## Architecture

```
OSMnx Road Graph (SF)
        │
        ▼
  Node Features          Edge Features
  [lat, lng,             [distance,
   is_warehouse,          is_active_route,
   demand_weight]         hour, weekday]
        │                      │
        └──────────┬───────────┘
                   ▼
            DeliveryGNN
         (2x GAT layers +
          BatchNorm + Dropout)
                   │
                   ▼
         Delay prediction
         per route (minutes)
                   │
                   ▼
       FastDeliveryRoutingEnv
       (Gymnasium environment)
                   │
                   ▼
            PPO Agent
      (keep route vs reroute)
                   │
                   ▼
        Optimized delivery plan
```

---

## Project structure

```
instacart_optimizer_gnn_rl/
│
├── SF_Delivery_Optimization.ipynb   # main Colab notebook (8 blocks)
│
└── drive/                           # auto-created on Google Drive
    ├── data/
    │   ├── graph/
    │   │   ├── sf_road_network.pkl       # OSMnx SF road graph
    │   │   └── sf_road_network.graphml
    │   ├── orders/
    │   │   └── orders.csv                # 16k simulated orders
    │   ├── warehouse_nodes.json          # snapped warehouse locations
    │   ├── neighborhood_nodes.json       # snapped neighborhood locations
    │   ├── route_distances.json          # shortest path distances (45 routes)
    │   └── delay_cache.pkl               # precomputed GNN predictions (7,560 entries)
    ├── models/
    │   ├── gnn_best.pt                   # best GNN checkpoint
    │   ├── gnn_final.pt
    │   ├── gnn_history.json              # training loss curves
    │   ├── node_scaler.pkl
    │   └── ppo_final.zip                 # trained PPO agent
    ├── checkpoints/                      # training checkpoints (auto-saved)
    ├── results/
    │   └── rl_eval.json                  # RL evaluation metrics
    ├── plots/
    │   ├── gnn_training_curves.png
    │   ├── rl_evaluation.png
    │   └── sf_delivery_map.html          # interactive Folium map
    └── config.json                       # shared config across sessions
```

---

## Quickstart

1. Open `SF_Delivery_Optimization.ipynb` in Google Colab
2. Set runtime to **GPU (T4)**
3. Run blocks 1–8 in order

All data, models, and checkpoints persist to Google Drive automatically. Rerunning any block after the first session loads from cache — no retraining needed.

---

## Stack

| Component | Library |
|---|---|
| Road network | OSMnx, NetworkX |
| GNN | PyTorch Geometric (GATConv) |
| RL agent | Stable-Baselines3 (PPO), Gymnasium |
| Map visualization | Folium |
| Data | NumPy, Pandas |
| Storage | Google Drive (persistent across Colab sessions) |

---

## Blocks

| Block | Description |
|---|---|
| 1 | Mount Google Drive, set up persistent storage |
| 2 | Install dependencies, imports, reproducibility |
| 3 | Download SF road network from OpenStreetMap, snap locations |
| 4 | Simulate Instacart-style order data (16k orders, 60 days) |
| 5 | Build PyG graph dataset (one graph per order) |
| 6 | Train DeliveryGNN (2x GAT + BatchNorm, 74k params) |
| 7 | Train PPO rerouting agent (200k timesteps, precomputed cache) |
| 8 | Interactive Folium map (delayed vs optimal vs RL-rerouted routes) |

---

## Key design decisions

**Why GNN?** Delivery delay depends on the entire road network state — not just one route in isolation. GNNs naturally model this by propagating congestion signals across neighboring nodes.

**Why precompute GNN predictions?** Running the GNN live inside the RL environment (6 forward passes per step) gives ~17 fps. Precomputing all 7,560 hour/day/route combinations and using dict lookups gives 2,000+ fps — making 200k training steps feasible in minutes instead of hours.

**Why PPO?** The action space is small (6 discrete actions) and episodes are single-step, making PPO a natural fit. The agent learns a policy over the continuous state space (delay predictions, hour, day, demand) that generalizes across all delivery scenarios.

---

## Limitations

- Order data is simulated, not real Instacart data
- GNN trained on simulated delay patterns — real GPS traces would improve accuracy
- RL agent has 5 alternative routes per decision — a larger action space could improve savings
- Map visualization is static to Friday 6pm — dynamic hour/day selector is a natural next step

---

## License

MIT
