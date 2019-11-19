create
```
conda create --name speech2gesture_env_py37 python=3.7 anaconda
```


start
```
activate speech2gesture_env_py37
```

extract
```
python -m data.train_test_data_extraction.extract_data_for_training --base_dataset_path ../ --speaker oliver
```



cuda:
```
wget http://developer.download.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda_10.1.243_418.87.00_linux.run

sudo sh cuda_10.1.243_418.87.00_linux.run
```
