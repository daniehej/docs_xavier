# Code for Jetson in CUDA
### Running CUDA under sudo

Some times you will need sudo for running programs and so on. However, the
sudo user can not by default use CUDA tools. In order to fix this, edit the file \"visudo\" eg by using nano
```
EDITOR=nano sudo visudo
```

At the end of the `secure_path`, add the following

```
:/usr/local/cuda-10.0/bin
```
so it will look something like 
```
secure\_path=\"/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/usr/local/cuda-10.0/bin\"
```

Sudo and root users can now see CUDA tools.

### Code, Compile, Run

In order to compile CUDA, we follow the example in <https://devblogs.nvidia.com/how-optimize-data-transfers-cuda-cc/>.

Start by making a new folder to put or files in so it's all
together, and go into that folder by doing so:
```
mkdir nvidia-test
cd nvidia-test
```

Now that we are in the folder, `nvidia-test`, we will make our new file,
we can use nano for that:

```
nano profile.cu
```

In the file put the following, and then save the file by pressing
\"Ctrl+O\" then \"Enter\" and exit the editor \"Ctrl+X\":

    int main()
    {
        const unsigned int N = 1048576;
        const unsigned int bytes = N * sizeof(int);
        int *h_a = (int*)malloc(bytes);
        int *d_a;
        cudaMalloc((int**)&d_a, bytes);

        memset(h_a, 0, bytes);
        cudaMemcpy(d_a, h_a, bytes, cudaMemcpyHostToDevice);
        cudaMemcpy(h_a, d_a, bytes, cudaMemcpyDeviceToHost);

        return 0;
    }

When the file is saved we can compile it by running the following:
```
nvcc profile.cu -o profile\_test
```
This compiles the file profile.cu and saves it as profile\_test which is
an executable, we can run that file by simply typing:

```
./profile\_test
```

In the example they are looking at how to optimize data transfers so
they use the tool \"nvprof\" to measure the performance of the
application,

```
nvprof ./profile\_test
```

You can try and run the \"BandwidthTest\" now on you own.
