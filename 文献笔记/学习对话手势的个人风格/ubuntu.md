create
```
conda create --name speech2gesture_env_py37 python=3.7 anaconda
```


start
```
source activate speech2gesture_env_py37

source activate speech2gesture_env_py27
```

extract
```
python -m data.train_test_data_extraction.extract_data_for_training --base_dataset_path ../ --speaker oliver
```

train
```
python -m audio_to_multiple_pose_gan.train --gans 1 --name test_run --arch_g audio_to_pose_gans --arch_d pose_D --speaker oliver --output_path ../tmp
```

```
python -m audio_to_multiple_pose_gan.predict_to_videos --train_csv ../train.csv --seq_len 64 --output_path ../tmp/my_output_folder --speaker oliver -ag audio_to_pose_gans --gans 1
```
---

tensorflow-gpu
```
https://files.pythonhosted.org/packages/a1/eb/bc0784af18f612838f90419cf4805c37c20ddb957f5ffe0c42144562dcfa/tensorflow_gpu-2.0.0-cp37-cp37m-manylinux2010_x86_64.whl
```

```
https://files.pythonhosted.org/packages/68/45/8ed49fb2decd4ce7849fc9755d9e066f414fb29c40e811bf4c12287de0af/tensorflow_gpu-1.9.0-cp27-cp27mu-manylinux1_x86_64.whl
```



---

cuda:
```
wget http://developer.download.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda_10.1.243_418.87.00_linux.run

sudo sh cuda_10.1.243_418.87.00_linux.run
```
