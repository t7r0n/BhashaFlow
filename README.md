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

### BLEU Scores for English to Indic Translations

| Language Pair       | BLEU Score | Detailed Score (n-grams)           | BP   | Ratio  | Hyp Len | Ref Len |
|---------------------|------------|-------------------------------------|------|--------|---------|---------|
| English to Assamese | 3.8        | 27.9/8.2/2.6/0.9                   | 0.793| 0.812  | 17070   | 21028   |
| English to Bengali  | 10.1       | 42.0/16.9/7.6/3.5                  | 0.862| 0.871  | 18420   | 21155   |
| English to Gujarati | 13.8       | 49.8/23.4/11.4/5.9                 | 0.828| 0.841  | 20061   | 23840   |
| English to Hindi    | 23.3       | 57.4/33.0/20.3/12.8                | 0.880| 0.887  | 24610   | 27743   |
| English to Kannada  | 9.0        | 43.5/15.6/6.7/3.1                  | 0.828| 0.841  | 15725   | 18687   |
| English to Malayalam| 6.8        | 42.2/14.2/5.6/2.3                  | 0.722| 0.754  | 13589   | 18020   |
| English to Marathi  | 7.7        | 42.0/15.5/6.4/2.8                  | 0.740| 0.769  | 16761   | 21810   |
| English to Odia     | 8.3        | 40.7/15.7/6.8/3.1                  | 0.770| 0.793  | 16756   | 21129   |
| English to Panjabi  | 15.9       | 50.8/24.5/12.9/7.1                 | 0.866| 0.874  | 23994   | 27451   |
| English to Telugu   | 11.1       | 48.6/19.8/9.3/4.6                  | 0.778| 0.799  | 16056   | 20096   |

### BLEU Scores for Indic to English Translations

| Language Pair        | BLEU Score | Detailed Score (n-grams)           | BP   | Ratio  | Hyp Len | Ref Len |
|----------------------|------------|-------------------------------------|------|--------|---------|---------|
| Assamese to English  | 17.8       | 49.8/22.9/12.3/7.1                 | 1.000| 1.038  | 25320   | 24390   |
| Bengali to English   | 22.1       | 55.7/27.9/15.9/9.6                 | 1.000| 1.040  | 25320   | 24341   |
| Gujarati to English  | 24.6       | 57.9/31.0/18.3/11.2                | 1.000| 1.039  | 25320   | 24361   |
| Hindi to English     | 27.1       | 59.6/33.4/20.7/13.1                | 1.000| 1.046  | 25320   | 24198   |
| Kannada to English   | 0.6        | 13.3/0.8/0.3/0.1                   | 0.772| 0.795  | 18781   | 23631   |
| Malayalam to English | 0.8        | 15.7/1.8/0.5/0.1                   | 0.715| 0.749  | 18107   | 24174   |
| Marathi to English   | 0.9        | 12.2/1.5/0.4/0.1                   | 0.889| 0.895  | 21884   | 24458   |
| Odia to English      | 0.5        | 6.6/0.7/0.3/0.1                    | 0.921| 0.924  | 22328   | 24168   |
| Panjabi to English   | 0.4        | 5.7/0.4/0.2/0.1                    | 1.000| 1.178  | 29308   | 24872   |
| Telugu to English    | 2.1        | 15.9/2.9/1.3/0.6                   | 0.844| 0.855  | 20213   | 23635   |


















