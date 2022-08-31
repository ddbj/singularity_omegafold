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
