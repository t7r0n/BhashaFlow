# BhashaFlow (113M)

BhashaFlow is a Neural Machine Translation (NMT) project translating between English and multiple Indic languages, leveraging custom transformer models built with Fairseq. The models are designed for efficient deployment and high performance, using a substantial parameter base and advanced evaluation metrics.

## Project Inspiration

This work is inspired by AI4Bharat's IndicTrans project, aiming to enhance language access across Indic languages.

## Dataset
The models are trained on the Samanantar dataset, a rich multilingual dataset designed for high-quality translation between English and Indic languages.

## Training Environment
Each model was trained on an RTX 2070 Max-Q GPU, with training times averaging around 30 hours per model due to the complex architecture and large parameter size.

## Supported Languages
English ↔ Assamese
English ↔ Bengali
English ↔ Gujarati
English ↔ Hindi
English ↔ Kannada
English ↔ Malayalam
English ↔ Marathi
English ↔ Odia
English ↔ Panjabi
English ↔ Telugu

## Performance Metrics
The performance is evaluated using BLEU scores, providing a robust measure of translation quality across language pairs. (Refer to Performance Metrics for detailed BLEU scores.)

## Training Parameters
The models were trained using Fairseq with the following key training parameters:

```bash
CUDA_VISIBLE_DEVICES=0 fairseq-train ../indic-en-exp/final_bin \
    --max-source-positions=100 \
    --max-target-positions=100 \
    --max-update=1000000 \
    --save-interval=1 \
    --arch=transformer \
    --criterion=label_smoothed_cross_entropy \
    --source-lang=SRC \
    --lr-scheduler=inverse_sqrt \
    --target-lang=TGT \
    --label-smoothing=0.1 \
    --optimizer adam \
    --adam-betas "(0.9, 0.98)" \
    --clip-norm 1.0 \
    --warmup-init-lr 1e-07 \
    --lr 0.0005 \
    --warmup-updates 2000 \
    --dropout 0.2 \
    --save-dir ../indic-en-exp/model \
    --keep-last-epochs 5 \
    --patience 5 \
    --skip-invalid-size-inputs-valid-test \
    --fp16 \
    --user-dir model_configs \
    --wandb-project 3fo \
    --update-freq=1 \
    --distributed-world-size 1 \
    --max-tokens 4096
```


## Performance Metrics
English to Indic and Indic to English translations have been evaluated with BLEU scores:

Language Pair	BLEU Score
English ↔ Assamese	7.8 / 23.8
English ↔ Bengali	13.1 / 28.1
English ↔ Gujarati	17.8 / 28.6
English ↔ Hindi	28.3 / 33.1
English ↔ Kannada	15.0 / 22.6
English ↔ Malayalam	11.8 / 20.8
English ↔ Marathi	12.7 / 24.9
English ↔ Odia	10.3 / 19.5
English ↔ Panjabi	28.9 / 16.4
English ↔ Telugu	21.1 / 12.1

















