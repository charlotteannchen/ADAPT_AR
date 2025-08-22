# ADAPT_AR

## Setup Environment
```bash
conda create -n llava python==3.10
conda activate llava
conda install pytorch=2.5.1 torchvision=0.20.1 torchaudio pytorch-cuda=12.4 -c pytorch -c nvidia -y 

git clone https://github.com/haotian-liu/LLaVA.git && cd LLaVA
pip install --no-deps -e .
cd ..

cp run_llava.py LLaVA/llava/eval/run_llava.py
cp llava_was.py LLaVA/llava_was.py
cp finetune_task_lora.sh LLaVA/scripts/v1_5/finetune_task_lora.sh
cp finetune_merge_lora.sh LLaVA/finetune_merge_lora.sh
```

## Dataset Format
```
[
  {
    "id": "trial_T20190909_040738_543042_3_Pot|-00.52|+00.83|+01.68_000000119",
    "image": "all_finetune_dataset_templated_pair_new/pot_dirty/trial_T20190909_040738_543042_3_Pot|-00.52|+00.83|+01.68_000000119.png",
    "conversations": [
      {
        "from": "human",
        "value": "<image>\n The image shows three pots: clean (left, single color), dirty (middle, with stains), and the query (right). Is the query pot used? Answer only 'yes' or 'no'."
      },
      {
        "from": "gpt",
        "value": "yes"
      }
    ]
  },
  ....
]
```

## Quick Start — LoRA Finetuning
```bash 
cd LLaVA
bash scripts/v1_5/finetune_task_lora.sh
```

## Merge weights after finetuning
```bash 
bash finetune_merge_lora.sh
```

## Training and validation dataset 
Full dataset will be released soon.
Small dataset can be found at all_finetune_dataset_all_templated_pair_random/. 

## Evaluation of Affordance Reasoning Capability
```bash
unzip all_finetune_dataset_all_templated_pair_random.zip
python eval_Affordance_Reasoning.py
```
