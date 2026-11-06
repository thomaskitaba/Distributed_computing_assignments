# Distributed_computing_assignments

Assignment 2 (Game of Life). Run from the answers folder:

make
./life -n 500 -i 200 -p 0.2 -t 4              # 4 compute threads + plotter, display on (needs gnuplot)
./life -n 2000 -i 100 -s 1 -p 0.3 -t 2 -d     # display off, fixed seed, for timing
./life -n 64 -i 100 -g 1 -d                   # block (still life)
./life -n 40 -i 60 -g 2                       # glider
./life -n 100 -i 50 -s 7 -t 3 -d -dump out.txt   # dump the final board so you can compare runs
make clean

Assignment 3 (cardiac simulation). Run from the project root:

make
./serial -n 1024 -t 100                                        # original serial baseline
mpirun -n 1 ./cardiacsim -n 1024 -t 100
mpirun -n 2 ./cardiacsim -n 1024 -t 100 -y 2                   # 1D geometry
mpirun -n 4 ./cardiacsim -n 400 -t 200 -x 2 -y 2               # 2D geometry
mpirun -n 4 ./cardiacsim -n 1024 -t 100 -k                     # communication off (timing only)
mpirun --bind-to none -n 2 ./cardiacsim -n 1024 -t 100 -y 2 -o 4   # hybrid: 2 processes x 4 threads
./cardiacsim -n 200 -t 1000 -p 100                             # one process, gnuplot every 100 time units
./run_studies.sh                                               # all three studies -> results.csv
cd visualization && python3 plot_results.py                    # figures

To check correctness, compare the printed Max and L2norm with ./serial for the same -n and -t.
