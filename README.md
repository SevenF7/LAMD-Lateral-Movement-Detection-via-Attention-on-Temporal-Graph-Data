# LAMD
## How to run the code
### Create folders
Create *data, log, results, saved_checkpoints, saved_models under* LAMD folder.
Run the following command if you are using Linux:

    mkdir data, log, results, saved_checkpoints, saved_models

### Preprocess the data
Paste auth dataset in *data* folder, then run:

    python utils/preprocess_data.py --data auth

### Start training

    python train_self_supervised.py --data auth

**Optional — direction-aware neighbors (Phase 0, for OHD-TGN/DIR-TGN):**  
To enable edge direction in the temporal neighbor finder (required for later direction-encoding improvements), add `--use_direction`:

    python train_self_supervised.py --data auth --use_direction

**Optional — OHD-TGN (Phase 1):**  
To add learned direction encoding to edge features (one embedding per direction, summed to ê_ij), add `--one_hot_dir`. This automatically enables direction in the neighbor finder:

    python train_self_supervised.py --data auth --one_hot_dir

**Optional — DIR-TGN (Phase 2):**  
To use two GNNs (out-edges and in-edges) and fuse with a learned α (`z = α·z_out + (1−α)·z_in`), add `--dir_gnn`. This automatically enables direction in the neighbor finder:

    python train_self_supervised.py --data auth --dir_gnn

Without `--use_direction` / `--one_hot_dir` / `--dir_gnn`, behavior is unchanged (undirected neighbors, no direction encoding). See `INTEGRATION_PLAN_PROVCTDG.md` for the integration plan.

Check the results in *log, results, saved_checkpoints, saved_models under* 

## Experimental data and results

Check (https://github.com/lostecho187/Experiments)
