
# Install 

```
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

# Run (`pipeline_a_segment` project)

```
dvc exp run -R pipeline_a_segment/x
dvc exp run -R pipeline_a_segment/y
dvc exp run -R pipeline_a_segment/z

```

## Run a pipeline (target/data/customer) 

`run.sh` script copies `dvc.yaml` template for a target division, and then runs a DVC pipeline.
 
```bash
./run.sh PROJECT TARGET 
```
Arguments:
- PROJECT - Path to a project/pipeline/model directory with a common `template_dvc.yaml`
- TARGET - Name of the target/data/customer to apply DVC pipeline to

Examples 
```bash
 # Run a segmentation pipeline for customer `x`
./run.sh pipeline_a_segment x
```

# Run multiple pipelines (list of targets)

Parse list of targets and run DVC pipeline for each of them
 
```bash
./run_targets.sh PROJECT TARGETS 
```
Arguments:
- PROJECT - Path to a project/pipeline/model directory with a common `template_dvc.yaml`
- TARGETS - Comma separated list of targets (no spaces in between)

Examples 
```bash
 # Run a detection pipeline for each target
./run_targets.sh pipeline_a_segment x,y,z
./run_targets.sh pipeline_b_detect i,j
```


# Changes

**Oct 16, 2023 - Add metrics tracking**
- metrics saved with DVCLive (in `ml/src/train.py` script)
- for project `pipeline_a_segment` - metrics saved in `PROJECT/dvclive/`, metrics/plot files automatically added to the root `dvc.yaml`, version with Git 
- for project `pipeline_b_detect` - metrics saved in `PROJECT/results/`, metrics/plot files specified in `dvc.yaml` (as outs in the `train` stage), version with DVC (not Git)
- in both cases DVC updates metrics/plots in Studio/VSCode in real time