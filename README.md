# singularity_omegafold
Ubuntu 20.04にomegafold v1.1.0をインストールしたsingularity imageを作成するためのSingularity definition fileです。
## imageのビルド
```
$ sudo singularity build omegafold-1.1.0.sif Singularity
```
## 遺伝研スパコン login_gpu.qでの実行
```
singularity exec --nv omegafold-1.1.0.sif python3 /opt/OmegaFold/main.py input.fasta output_dir
```
カレントディレクトリに output_dir が作成され、その中に結果が出力されます。

## 遺伝研スパコン intel.qでの実行用ジョブスクリプト
```
#!/bin/bash
#$ -S /bin/sh
#$ -cwd
#$ -l s_vmem=2G
#$ -l mem_req=2G
#$ -l intel
#$ -pe def_slot 16
N=16
singularity exec /home/y-okuda/singularity/omegafold/omegafold-1.1.0.sif \
sh -c "\
export OMP_NUM_THREADS=${N}; \
python3 /opt/OmegaFold/main.py \
--device cpu \
/home/y-okuda/singularity/omegafold/HSA.fasta \
/home/y-okuda/singularity/omegafold/output_dir \
"
```
Nに設定した数のCPUコアを使用します。同じ値を -pe def_slot にも設定してください。
