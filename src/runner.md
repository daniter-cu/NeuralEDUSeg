# Running on slurm

nlprun -g 1 -a iter-eduseg -n eduseg1 -o eduseg1.job "python run.py --segment --input_files ../../../usrc/data/wiki4b1-0.txt --result_dir ../../../usrc/data/eduseped"
