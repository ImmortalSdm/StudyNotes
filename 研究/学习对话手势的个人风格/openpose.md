下载源码
```
git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose.git
```

检查是否需要更新
```
git pull origin master
```

安装cmake-gui
```
sudo apt-get install cmake-qt-gui
```

下载模型
```
cd models
./getModels.sh
```

创建build文件
```
cd ..
mkdir build
```

---

## opencv
```
sudo apt update
sudo apt upgrade
sudo apt install libopencv-dev python-opencv

pkg-config --modversion opencv
```
---
## caffe
#### 依赖库
```
sudo apt-get --assume-yes install build-essential
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install --no-install-recommends libboost-all-dev
#将遇到依赖问题
```

解决问题
```
sudo apt-get install aptitude

# n 会给出第二种解决方案
sudo aptitude install libboost-all-dev
```

```
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install libopenblas-dev liblapack-dev libatlas-base-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev

# Python libs
sudo apt install python-pip

sudo -H pip install --upgrade numpy protobuf

```
---

#### 正式安装caffe
```
git clone https://github.com/BVLC/caffe.git
```

用unzip命令解压
```
unzip caffe-master.zip
```

重命名为caffe
```
mv caffe-master caffe
```

切换到caffe所在的目录
```
cd caffe
```
---


首先将Makefile.config.example的内容复制到Makefile.config，因为make指令只能make Makefile.config文件，而Makefile.config.example是caffe给出的makefile例子
```
sudo cp Makefile.config.example Makefile.config
```

#### 修改配置文件Makefile.config：
```
sudo vim Makefile.config
```

- 应用 cudnn，将`#USE_CUDNN := 1`修改成`USE_CUDNN := 1`
- 应用 opencv 版本 如果opencv的版本是3。那么将#OPENCV_VERSION := 3 修改为：OPENCV_VERSION := 3
- 使用 python 接口，将`#WITH_PYTHON_LAYER := 1`修改为`WITH_PYTHON_LAYER := 1`
- `INCLUDE_DIRS:= $(PYTHON_INCLUDE) /usr/local/include`修改为`INCLUDE_DIRS:= $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial`
- `LIBRARY_DIRS:= $(PYTHON_LIB) /usr/local/lib /usr/lib`修改为`LIBRARY_DIRS:= $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/usr/lib/x86_64-linux-gnu/hdf5/serial`

#### 修改Makefile文件
```
sudo vim Makefile
```
- 将
`NVCCFLAGS +=-ccbin=$(CXX) -Xcompiler-fPIC$(COMMON_FLAGS)`
替换为
`NVCCFLAGS += -D_FORCE_INLINES -ccbin=$(CXX) -Xcompiler -fPIC $(COMMON_FLAGS)`
- 将`LIBRARIES += hdf5_hl hdf5`
改为`LIBRARIES += hdf5_serial_hl hdf5_serial`

#### host_config.h
```
sudo vim /usr/local/cuda/include/crt/host_config.h
```

将
```
#error-- unsupported GNU version! gcc versionslater than 6 are not supported!
```
改为
```
//#error-- unsupported GNU version! gcc versionslater than 6 are not supported!
```
---
### 错误解决
```
sudo vim Makefile
```

- 添加`-std=c++11`至如下位置处：
![img](https://img-blog.csdnimg.cn/20191023165259670.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMDExMjc3,size_16,color_FFFFFF,t_70)

---

报大错哦
```
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::InitializationErrorString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteStringMaybeAliased(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::AssignDescriptors(std::string const&, google::protobuf::internal::MigrationSchema const*, google::protobuf::Message const* const*, unsigned int const*, google::protobuf::Metadata*, google::protobuf::EnumDescriptor const**, google::protobuf::ServiceDescriptor const**)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::io::CodedOutputStream::WriteStringWithSizeToArray(std::string const&, unsigned char*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::GetTypeName() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::DebugString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::MessageLite::ParseFromString(std::string const&)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::NameOfEnum(google::protobuf::EnumDescriptor const*, int)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::ReadBytes(google::protobuf::io::CodedInputStream*, std::string*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::MessageFactory::InternalRegisterGeneratedFile(char const*, void (*)(std::string const&))'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::DB::Open(leveldb::Options const&, std::string const&, leveldb::DB**)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteBytesMaybeAliased(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::fixed_address_empty_string'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::Status::ToString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteString(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
collect2: error: ld returned 1 exit status
make: *** [Makefile:638：.build_release/tools/upgrade_net_proto_text.bin] 错误 1
make: *** 正在等待未完成的任务....
/usr/bin/ld: .build_release/tools/caffe.o: in function `std::string* google::MakeCheckOpString<cudaError, cudaError>(cudaError const&, cudaError const&, char const*)':
caffe.cpp:(.text._ZN6google17MakeCheckOpStringI9cudaErrorS1_EEPSsRKT_RKT0_PKc[_ZN6google17MakeCheckOpStringI9cudaErrorS1_EEPSsRKT_RKT0_PKc]+0x43): undefined reference to `google::base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/tools/caffe.o: in function `std::string* google::MakeCheckOpString<unsigned long, int>(unsigned long const&, int const&, char const*)':
caffe.cpp:(.text._ZN6google17MakeCheckOpStringImiEEPSsRKT_RKT0_PKc[_ZN6google17MakeCheckOpStringImiEEPSsRKT_RKT0_PKc]+0x43): undefined reference to `google::base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/tools/caffe.o: in function `main':
caffe.cpp:(.text.startup+0x3e): undefined reference to `google::SetVersionString(std::string const&)'
/usr/bin/ld: caffe.cpp:(.text.startup+0x6e): undefined reference to `google::SetUsageMessage(std::string const&)'
/usr/bin/ld: .build_release/tools/caffe.o: in function `_GLOBAL__sub_I_caffe.cpp':
caffe.cpp:(.text.startup+0x3b4): undefined reference to `google::FlagRegisterer::FlagRegisterer<std::string>(char const*, char const*, char const*, std::string*, std::string*)'
/usr/bin/ld: caffe.cpp:(.text.startup+0x460): undefined reference to `google::FlagRegisterer::FlagRegisterer<std::string>(char const*, char const*, char const*, std::string*, std::string*)'
/usr/bin/ld: caffe.cpp:(.text.startup+0x505): undefined reference to `google::FlagRegisterer::FlagRegisterer<std::string>(char const*, char const*, char const*, std::string*, std::string*)'
/usr/bin/ld: caffe.cpp:(.text.startup+0x5aa): undefined reference to `google::FlagRegisterer::FlagRegisterer<std::string>(char const*, char const*, char const*, std::string*, std::string*)'
/usr/bin/ld: caffe.cpp:(.text.startup+0x67e): undefined reference to `google::FlagRegisterer::FlagRegisterer<std::string>(char const*, char const*, char const*, std::string*, std::string*)'
/usr/bin/ld: .build_release/tools/caffe.o:caffe.cpp:(.text.startup+0x723): more undefined references to `google::FlagRegisterer::FlagRegisterer<std::string>/usr/bin/ld: .build_release/examples/cpp_classification/classification.o: in function `std::string* google::MakeCheckOpString<int, int>(int const&, int const&, char const*)':
classification.cpp:(.text._ZN6google17MakeCheckOpStringIiiEEPSsRKT_RKT0_PKc[_ZN6google17MakeCheckOpStringIiiEEPSsRKT_RKT0_PKc]+0x43): undefined reference to `google::base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/examples/cpp_classification/classification.o: in function `std::string* google::MakeCheckOpString<unsigned long, int>(unsigned long const&, int const&, char const*)':
classification.cpp:(.text._ZN6google17MakeCheckOpStringImiEEPSsRKT_RKT0_PKc[_ZN6google17MakeCheckOpStringImiEEPSsRKT_RKT0_PKc]+0x43): undefined reference to `google::base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::InitializationErrorString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteStringMaybeAliased(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::AssignDescriptors(std::string const&, google::protobuf::internal::MigrationSchema const*, (google::protobuf::Message const* const*, unsigned int const*, google::protobuf::charMetadata /usr/bin/ld: .build_release/*tools/compute_image_mean.o: in function `std::string* google::MakeCheckOpString<int, int>,(int const&, int const&, char const*)':
compute_image_mean.cpp:(.text._ZN6google17MakeCheckOpStringIiiEEPSsRKT_RKT0_PKc[_ZN6google17MakeCheckOpStringIiiEEPSsRKT_RKT0_PKc]+0x43): undefined reference to `google::base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/tools/compute_image_mean.o: in function `std::string* google::MakeCheckOpString<unsigned long, int>(unsigned long const&, int const&, char const*)':
compute_image_mean.cpp:(.text._ZN6google17MakeCheckOpStringImiEEPSsRKT_RKT0_PKc[_ZN6google17MakeCheckOpStringImiEEPSsRKT_RKT0_PKc]+0x43): undefined reference to `google::base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/tools/compute_image_mean.o: in function `_GLOBAL__sub_I_compute_image_mean.cpp':
compute_image_mean.cpp:(.text.startup+0x8b): undefined reference to `google::FlagRegisterer::FlagRegisterer<std::string>(char const*, char const*, char const*, std::string*, std::string*)'
/usr/bin/ld: .build_release/tools/compute_image_mean.o: in function ` main':google
compute_image_mean.cpp:::(protobuf.:text.startup:+EnumDescriptor0x13f )const:* *undefined,  referencegoogle :to: protobuf`google::::ServiceDescriptorSetUsageMessage (conststd*:*:)string'
const/&/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::InitializationErrorString()) const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteStringMaybeAliased(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::AssignDescriptors(std::string const&, google::protobuf::internal::MigrationSchema const*, google::protobuf::Message const* const*, unsigned int const*, google::protobuf::Metadata*, google::protobuf::EnumDescriptor const**, google::protobuf::ServiceDescriptor const**)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::io::CodedOutputStream::WriteStringWithSizeToArray(std::string const&, unsigned char*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::GetTypeName() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::DebugString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::MessageLite::ParseFromString(std::string const&)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::NameOfEnum(google::protobuf::EnumDescriptor const*, int)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::ReadBytes(google::protobuf::io::CodedInputStream*, std::string*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::MessageFactory::InternalRegisterGeneratedFile(char const*, void (*)(std::string const&))'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::DB::Open(leveldb::Options const&, std::string const&, leveldb::DB**)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteBytesMaybeAliased(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::fixed_address_empty_string'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::Status::ToString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteString(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
collect2: error: ld returned 1 exit status
usr'const*
,/usr /charbin /constld*:,  compute_image_mean.cppchar :const(*.,text.startup +std0x23a:)::string *undefined,make: *** [Makefile:638：.build_release/tools/upgrade_solver_proto_text.bin] 错误 1
  stdreference: :tostring *`)google': :followprotobuf
:/:usrMessageLite/:bin:/ParseFromStringld(:std :.:build_releasestring/ libconst/&libcaffe.so):'
undefined /referenceusr /tobin /`ldgoogle:: :compute_image_mean.cppprotobuf::(:.Messagetext.startup:+:0x3c9InitializationErrorString)(:)  undefinedconst 'reference
 /tousr /`bingoogle/:ld::protobuf :.:build_releaseMessageLite/:lib:/ParseFromStringlibcaffe.so(:std :undefined: stringreference  toconst &`)google'
:/:usrprotobuf/:bin:/internalld::: WireFormatLite.:build_release:/WriteStringMaybeAliasedlib(/intlibcaffe.so,:  stdundefined: :referencestring  toconst &,` googlegoogle::::protobufprotobuf::::Messageio::::InitializationErrorStringCodedOutputStream(*)) '
const/'usr
//binusr//ldbin:/ ld.:build_release /.libbuild_release//libcaffe.solib:/ libcaffe.soundefined:  referenceundefined  toreference  `togoogle :`:googleprotobuf::::internalprotobuf::::AssignDescriptorsinternal(:std::WireFormatLite::string: WriteStringMaybeAliasedconst(&int,,  googlestd::::protobufstring: :constinternal&:,: MigrationSchemagoogle :const:*protobuf,: :googleio::::protobufCodedOutputStream:*:)Message'
const/*usr /constbin*/,ld :unsigned  .intbuild_release const/*lib,/ libcaffe.sogoogle:: :undefinedprotobuf :reference: Metadatato* ,` googlegoogle::::protobufprotobuf::::internalEnumDescriptor: :constAssignDescriptors*(*std,: :googlestring: :constprotobuf:&:,ServiceDescriptor  googleconst:*:*protobuf):':internal
:/:usrMigrationSchema/ binconst/*ld,:  google.:build_release:/libprotobuf/:libcaffe.so::Message  undefinedconst *reference  constto* ,` googleunsigned: :intprotobuf :const:*io,: :googleCodedOutputStream::::protobufWriteStringWithSizeToArray:(:stdMetadata:*:,string  googleconst:&:,protobuf :unsigned: EnumDescriptorchar *const)*'
*/,usr /googlebin:/:ldprotobuf:: :.ServiceDescriptorbuild_release /constlib*/*libcaffe.so):'
/undefined reference usrto /`bingoogle/:ld::protobuf :.:build_releaseMessage/:lib:/GetTypeNamelibcaffe.so(:)  undefinedconst 'reference
 /tousr /`bingoogle/:ld::protobuf :.:iobuild_release:/:libCodedOutputStream/:libcaffe.so::WriteStringWithSizeToArray (undefinedstd :reference: stringto  `const&google,: :unsignedprotobuf :/:binchar/ld: *.build_release/Messagelib/libcaffe.so: undefined :reference to `)google::protobuf::io:::CodedOutputStream:':WriteStringWithSizeToArray(DebugStringstd:
:string( const)&, unsigned char*/) '
/usrusr/binconst/ld:/ .build_release/lib'/libcaffe.so: undefined referencebin to
 `google::protobuf::Message/::GetTypeName/(usr) const'
ld/usr/bin/:ld: .build_release//libbin/libcaffe.so: undefined reference  to `google/::protobuf::Message.build_release::DebugString(ld): const'
// usr/bin/ld:lib ..build_release/lib/libcaffe.so:build_release undefined reference/ libcaffe.soto `google:/:protobuf:::MessageLite::ParseFromString(libstd: undefined:string const/&)'
/libcaffe.sousr/bin/ld : .build_release/libreference:/libcaffe.so:  undefined reference to undefined  `google:to:protobuf::internal:: NameOfEnum(google:reference:`protobuf:: EnumDescriptorgoogle const*,to  int)'
/usr/bin/ld:: `.build_release/lib:/libcaffe.sogoogle: protobufundefined :reference :to :`google:::protobufprotobuf:Message:internal:::WireFormatLite::ReadBytes(:google:::protobuf::io::CodedInputStream:*,MessageLite std:::string*)'GetTypeName
/usr/:bin/ld:( ParseFromString.build_release/lib/libcaffe.so: )undefined reference( to  `stdgoogle::protobuf::MessageFactoryconst::InternalRegisterGeneratedFile:('char const*:, voidstring
 (*)(std/: :string constusr&))'
const/usr/bin/ld&: ./build_release/lib/libcaffe.so: )undefined referencebin to `leveldb:/ld':DB:
:Open(leveldb:::Options const/&, std:: string const&usr,. leveldb::DB*/*)'
/usrbuild_release/bin/binld: .build_release/lib/libcaffe.so/: undefined/ reference to `googlelib::protobuf:ld:internal/:::WireFormatLite:: WriteBytesMaybeAliased(int,libcaffe.so .std::string: constbuild_release&, google ::/protobuf::ioundefined ::CodedOutputStream*)lib'
/usr//bin/ld: .libcaffe.soreferencebuild_release /lib/libcaffe.so: :undefined reference to `togoogle ::protobuf:: internal::fixed_address_empty_stringundefined'
/usr/bin/ld`: . build_release/lib/libcaffe.so:reference  undefined reference to `leveldbgoogle::Status:::ToString() const'to
/usr/:bin/ld:  .build_release/libprotobuf/libcaffe.so`: undefined reference: to `googlegoogle::protobuf:::internal:::WireFormatLite::WriteString:protobuf(int, stdMessage::string const:&, google::protobuf:::io:::CodedOutputStream*)'DebugString(:
internal:): NameOfEnumconst('google
:/:usrprotobuf/:bin:/EnumDescriptorld :constcollect2: error: ld returned 1 exit status
 *.,build_release /intlib)/'libcaffe.so
:/ usrundefined/ binreference/ ldto:  `.googlebuild_release:/:libprotobuf/:libcaffe.so:internal: :undefined: NameOfEnumreference( googleto: :`protobufgoogle::::EnumDescriptorprotobuf const:*:,make: *** [Makefile:643：.build_release/examples/cpp_classification/classification.bin] 错误 1
 internalint:):'WireFormatLite
:/:usrReadBytes/(bingoogle/:ld::protobuf :.:build_releaseio/:lib:/CodedInputStreamlibcaffe.so*:,  undefinedstd :reference: stringto* )`'google
:/:usrprotobuf/:bin:/internalld::: WireFormatLite.:build_release:ReadBytes/(libgoogle/libcaffe.so::: protobufundefined: :referenceio: :toCodedInputStream *`,google :std::protobuf::string:*MessageFactory):':
InternalRegisterGeneratedFile/(usrchar/ binconst/*ld,:  void. build_release(/*lib)/(libcaffe.sostd:: :undefinedstring  referenceconst &to) )`'google
:/:usrprotobuf/:bin:/MessageFactoryld::: InternalRegisterGeneratedFile.(build_releasechar/ libconst/*libcaffe.so,:  undefinedvoid  reference(*) (tostd :`:leveldbstring :const:&DB):):'Open
(/leveldbusr:/:binOptions/ ldconst:& ,. build_releasestd/:lib:/stringlibcaffe.so :const &undefined,  referenceleveldb :to: DB`*leveldb*:):'DB
:/:usrOpen/(binleveldb/:ld::Options  .constbuild_release&/,lib /stdlibcaffe.so::: stringundefined  constreference& ,to  leveldb`:google::DB:*protobuf*:):'internal
:/:usrWireFormatLite/:bin:/WriteBytesMaybeAliasedld(:int .,build_release/ libstd/:libcaffe.so::string  undefinedconst &reference,  togoogle :`:googleprotobuf::::protobufio::::internalCodedOutputStream:*:)WireFormatLite':
:/WriteBytesMaybeAliasedusr(/binint/,ld :std :.:build_releasestring/ libconst/&libcaffe.so,:  googleundefined: :referenceprotobuf :to: io`:google::CodedOutputStream:*protobuf):':
internal/:usr:/fixed_address_empty_stringbin'/
ld/:usr /.binbuild_release//ldlib:/ libcaffe.so.:build_release /undefinedlib /referencelibcaffe.so :to  undefined` googlereference :to: protobuf`:leveldb::internal::Status::fixed_address_empty_string:'ToString
/(usr)/ binconst'/
ld/:usr /.binbuild_release//ldlib:/ libcaffe.so.:build_release /undefinedlib /referencelibcaffe.so :to  undefined` leveldbreference: :toStatus :`:googleToString(:): protobufconst:':
internal/:usr:/WireFormatLitebin:/:ldWriteString:( int.,build_release /stdlib:/:libcaffe.sostring:  constundefined& ,reference  googleto: :`protobufgoogle::::ioprotobuf::::CodedOutputStreaminternal*:):'WireFormatLite
:collect2: error: ld returned 1 exit status
:WriteString(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
collect2: error: ld returned 1 exit status
make: *** [Makefile:638：.build_release/tools/caffe.bin] 错误 1
/usr/bin/ld: .build_release/tools/extract_features.o: in function `std::string* google::MakeCheckOpString<int, int>(int const&, int const&, char const*)':
extract_features.cpp:(.text._ZN6google17MakeCheckOpStringIiiEEPSsRKT_RKT0_PKc[_ZN6google17MakeCheckOpStringIiiEEPSsRKT_RKT0_PKc]+0x43): undefined reference to `google::base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/tools/extract_features.o: in function `std::string* google::MakeCheckOpString<unsigned long, unsigned long>(unsigned long const&, unsigned long const&, char const*)':
extract_features.cpp:(.text._ZN6google17MakeCheckOpStringImmEEPSsRKT_RKT0_PKc[_ZN6google17MakeCheckOpStringImmEEPSsRKT_RKT0_PKc]+0x44): undefined reference to `google::base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/tools/extract_features.o: in function `int feature_extraction_pipeline<float>(int, char**)':
extract_features.cpp:(.text._Z27feature_extraction_pipelineIfEiiPPc[_Z27feature_extraction_pipelineIfEiiPPc]+0xb88): undefined reference to `google::protobuf::internal::fixed_address_empty_string'
/usr/bin/ld: extract_features.cpp:(.text._Z27feature_extraction_pipelineIfEiiPPc[_Z27feature_extraction_pipelineIfEiiPPc]+0x117d): undefined reference to `google::protobuf::MessageLite::SerializeToString(std::string*) const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::InitializationErrorString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteStringMaybeAliased(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::AssignDescriptors(std::string const&, google::protobuf::internal::MigrationSchema const*, google::protobuf::Message const* const*, unsigned int const*, google::protobuf::Metadata*, google::protobuf::EnumDescriptor const**, google::protobuf::ServiceDescriptor const**)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::io::CodedOutputStream::WriteStringWithSizeToArray(std::string const&, unsigned char*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::GetTypeName() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::DebugString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::MessageLite::ParseFromString(std::string const&)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::NameOfEnum(google::protobuf::EnumDescriptor const*, int)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::ReadBytes(google::protobuf::io::CodedInputStream*, std::string*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::MessageFactory::InternalRegisterGeneratedFile(char const*, void (*)(std::string const&))'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::DB::Open(leveldb::Options const&, std::string const&, leveldb::DB**)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteBytesMaybeAliased(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::Status::ToString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteString(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
collect2: error: ld returned 1 exit status
/usr/bin/ldmake: *** [Makefile:638：.build_release/tools/compute_image_mean.bin] 错误 1
: .build_release/examples/mnist/convert_mnist_data.o: in function make: *** [Makefile:638：.build_release/tools/extract_features.bin] 错误 1
`convert_dataset(char const*, char const*, char const*, std::string const&)':
convert_mnist_data.cpp:(.text+0x705): undefined reference to `google::protobuf::MessageLite::SerializeToString(std::string*) const'
/usr/bin/ld: convert_mnist_data.cpp:(.text+0x7dc): undefined reference to `google::protobuf::internal::fixed_address_empty_string'
/usr/bin/ld: .build_release/examples/mnist/convert_mnist_data.o: in function `std::string* google::MakeCheckOpString<unsigned int, int>(unsigned int const&, int const&, char const*)':
convert_mnist_data.cpp:(.text._ZN6google17MakeCheckOpStringIjiEEPSsRKT_RKT0_PKc[_ZN6google17MakeCheckOpStringIjiEEPSsRKT_RKT0_PKc]+0x43): undefined reference to `google::base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/examples/mnist/convert_mnist_data.o: in function `std::string* google::MakeCheckOpString<unsigned int, unsigned int>(unsigned int const&, unsigned int const&, char const*)':
convert_mnist_data.cpp:(.text._ZN6google17MakeCheckOpStringIjjEEPSsRKT_RKT0_PKc[_ZN6google17MakeCheckOpStringIjjEEPSsRKT_RKT0_PKc]+0x43): undefined reference to `google::base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/examples/mnist/convert_mnist_data.o: in function `_GLOBAL__sub_I_convert_mnist_data.cpp':
convert_mnist_data.cpp:(.text.startup+0x8b): undefined reference to `google::FlagRegisterer::FlagRegisterer<std::string>(char const*, char const*, char const*, std::string*, std::string*)'
/usr/bin/ld: .build_release/examples/mnist/convert_mnist_data.o: in function `main':
convert_mnist_data.cpp:(.text.startup+0x114): undefined reference to `google::SetUsageMessage(std::string const&)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::InitializationErrorString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteStringMaybeAliased(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::AssignDescriptors(std::string const&, google::protobuf::internal::MigrationSchema const*, google::protobuf::Message const* const*, unsigned int const*, google::protobuf::Metadata*, google::protobuf::EnumDescriptor const**, google::protobuf::ServiceDescriptor const**)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::io::CodedOutputStream::WriteStringWithSizeToArray(std::string const&, unsigned char*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::GetTypeName() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::DebugString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::MessageLite::ParseFromString(std::string const&)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::NameOfEnum(google::protobuf::EnumDescriptor const*, int)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::ReadBytes(google::protobuf::io::CodedInputStream*, std::string*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::MessageFactory::InternalRegisterGeneratedFile(char const*, void (*)(std::string const&))'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::DB::Open(leveldb::Options const&, std::string const&, leveldb::DB**)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteBytesMaybeAliased(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::Status::ToString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteString(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
collect2: error: ld returned 1 exit status
make: *** [Makefile:643：.build_release/examples/mnist/convert_mnist_data.bin] 错误 1
/usr/bin/ld: .build_release/tools/convert_imageset.o: in function `std::string* google::MakeCheckOpString<unsigned long, int>(unsigned long const&, int const&, char const*)':
convert_imageset.cpp:(.text._ZN6google17MakeCheckOpStringImiEEPSsRKT_RKT0_PKc[_ZN6google17MakeCheckOpStringImiEEPSsRKT_RKT0_PKc/usr/]bin+0x43): undefined /referenceld: .build_release/lib/ libcaffe.so: undefined reference to `togoogle::protobuf::Message::InitializationErrorString() const'
 /usr`/bin/ld: .google:build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteStringMaybeAliased(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::AssignDescriptors(std::string const&, google::protobuf::internal::MigrationSchema const*, google::protobuf::Message const* const*,:base::CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/tools/convert_imageset.o: in function `_GLOBAL__sub_I_convert_imageset.cpp':
convert_imageset.cpp unsigned int const*, google::protobuf::Metadata*, google::protobuf::EnumDescriptor :(.text.startup+0xef): undefined reference to `google::FlagRegisterer::FlagRegisterer<std::string>(char const*, char const*, char const*, std::string*, std::string*)const**, google::protobuf::ServiceDescriptor const**)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined'
/usr/bin/ld: convert_imageset.cpp:(.text.startup+0x250): undefined reference to `google::FlagRegisterer: reference to `google::protobuf::io::CodedOutputStream::WriteStringWithSizeToArray(std::string const&, unsigned char*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference :FlagRegisterer<std::string>(char const*, char const*, char const*, std::string*, std::string*)'
/usr/bin/ld: .build_release/tools/convert_imageset.oto `google::protobuf::Message::GetTypeName() const'
/usr/bin/ld: .build_release/lib: in function `main':
convert_imageset.cpp:(/libcaffe.so: undefined reference to `google::base:.text.startup+0x313): undefined:CheckOpMessageBuilder::NewString()'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference  reference to `google::SetUsageMessage(std::string const&)'
/usr/bin/ld: convert_imageset.cppto `google::protobuf::Message::DebugString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference :(.text.startup+0xc02): undefined reference to `google::protobuf::MessageLite::SerializeToString(std::string*) const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::to `google::protobuf::MessageLite::ParseFromString(std::string const&)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::InitializationErrorString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal:internal::NameOfEnum(google::protobuf::EnumDescriptor const*, int)'
/usr/bin/ld: .:WireFormatLite::WriteStringMaybeAliased(int, std::string const&, google::build_release/lib/libcaffe.so: undefined reference to protobuf::io::CodedOutputStream*)'
`google::protobuf::internal::WireFormatLite::ReadBytes(google::protobuf/usr/bin/ld: .build_release/lib/libcaffe.so: undefined::io::CodedInputStream*, std::string*)'
 reference to `google::protobuf::internal::AssignDescriptors(std::string const&, google::protobuf::internal::MigrationSchema const*, google:/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::MessageFactory::InternalRegisterGeneratedFile(char const*, void (*)(std::string const&))'
/usr/bin/ld:protobuf::Message const* const*, unsigned int const*, google::protobuf::Metadata*, google::protobuf::EnumDescriptor const**, google::: .build_release/lib/libcaffe.so: undefined reference to protobuf::ServiceDescriptor const**)'
/usr/bin/ld: .build_release/lib/`leveldb::DB::Open(leveldb::Options const&, std::string const&, leveldb::DBlibcaffe.so: undefined reference to `google::protobuf::io::CodedOutputStream::WriteStringWithSizeToArray(std::string const&**)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference , unsigned char*)'
/usr/bin/ld: to `google::protobuf::internal::WireFormatLite::WriteBytesMaybeAliased(int, std:.build_release/lib/libcaffe.so: undefined reference to `google::protobuf::Message::GetTypeName() :string const&, google::protobuf::io::CodedOutputStream*)'
/usr/bin/ld: .const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefinedbuild_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::fixed_address_empty_string'
/usr/bin/ld reference to `google::protobuf::Message::DebugString() const'
/usr: .build_release/lib/libcaffe.so: undefined reference to `leveldb::Status::ToString() const'/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::MessageLite::
/usr/bin/ld: .build_release/ParseFromString(std::string const&lib/libcaffe.so: undefined reference to `google::protobuf::)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined internal::WireFormatLite::WriteString(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
collect2: error: ld returned 1 exit status
reference to `google::protobuf::internal::NameOfEnum(google::protobuf::EnumDescriptor const*, int)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::ReadBytes(google::protobuf::io::CodedInputStream*, std::string*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::MessageFactory::InternalRegisterGeneratedFile(char const*, void (*)(std::string const&))'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::DB::Open(leveldb::Options const&, std::string const&, leveldb::DB**)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteBytesMaybeAliased(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::fixed_address_empty_string'
/make: *** [Makefile:638：.build_release/tools/upgrade_net_proto_binary.bin] 错误 1
usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::Status::ToString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteString(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
collect2: error: ld returned 1 exit status
make: *** [Makefile:638：.build_release/tools/convert_imageset.bin] 错误 1
/usr/bin/ld: .build_release/examples/cifar10/convert_cifar_data.o: in function `convert_dataset(std::string const&, std::string const&, std::string const&)':
convert_cifar_data.cpp:(.text+0x94a): undefined reference to `google::protobuf::internal::fixed_address_empty_string'
/usr/bin/ld: convert_cifar_data.cpp:(.text+0x98a): undefined reference to `google::protobuf::MessageLite::SerializeToString(std::string*) const'
/usr/bin/ld: convert_cifar_data.cpp:(.text+0x11b6): undefined reference to `google::protobuf::internal::fixed_address_empty_string'
/usr/bin/ld/:usr /convert_cifar_data.cppbin:/(ld.:text +.0x11f6build_release)/:examples /undefinedsiamese /referenceconvert_mnist_siamese_data.o :to  in` googlefunction: :`protobufconvert_dataset:(:charMessageLite :const:*SerializeToString,( stdchar: :conststring**,)  charconst 'const
*/)usr'/:bin
/convert_mnist_siamese_data.cppld::( ..textbuild_release+/0x4cdlib)/:libcaffe.so :undefined  undefinedreference  referenceto  to` leveldb`:google::DB::protobuf::Open:(Messageleveldb::::InitializationErrorStringOptions( )const &const,'
std/:usr:/stringbin /constld&:,  .leveldbbuild_release:/:libDB/*libcaffe.so*:) 'undefined
 /referenceusr /tobin /`ldgoogle:: :convert_mnist_siamese_data.cppprotobuf::(:.internaltext:+:0x8faWireFormatLite)::: WriteStringMaybeAliasedundefined( intreference,  tostd :`:googlestring: :constprotobuf&:,: internalgoogle::::fixed_address_empty_stringprotobuf':
:/iousr:/:binCodedOutputStream/*ld):'
convert_mnist_siamese_data.cpp/:usr(/.bintext/+ld0x951:) :. build_releaseundefined/ libreference/ libcaffe.soto:  `undefinedgoogle :reference: protobufto: :`MessageLitegoogle::::SerializeToStringprotobuf(:std::internal::string:*AssignDescriptors)( stdconst:':
string/ usrconst/&bin,/ ldgoogle:: :.protobufbuild_release:/:examplesinternal/:siamese:/MigrationSchemaconvert_mnist_siamese_data.o :const *in,  functiongoogle :`:stdprotobuf::::stringMessage*  constgoogle*: :constMakeCheckOpString*<,unsigned  unsignedint ,int  intconst>*(,unsigned  googleint: :constprotobuf&:,: Metadataint* ,const &google,: :charprotobuf :const:*EnumDescriptor) 'const:*
*convert_mnist_siamese_data.cpp,: (google.:text._ZN6google17MakeCheckOpStringIjiEEPSsRKT_RKT0_PKc:[protobuf_ZN6google17MakeCheckOpStringIjiEEPSsRKT_RKT0_PKc:]:+ServiceDescriptor0x43 )const:* *undefined) 'reference
 /tousr /`bingoogle/:ld::base :.:build_releaseCheckOpMessageBuilder/:lib:/NewStringlibcaffe.so(:) 'undefined
 /referenceusr /tobin /`ldgoogle:: :.protobufbuild_release:/:examplesio/:siamese:/CodedOutputStreamconvert_mnist_siamese_data.o::: WriteStringWithSizeToArrayin( stdfunction: :`stringstd :const:&string,*  unsignedgoogle :char:*MakeCheckOpString)<'unsigned
 /intusr,/ binunsigned/ ldint:> (.unsignedbuild_release /intlib /constlibcaffe.so&:,  undefinedunsigned  referenceint  toconst &`,google :char: protobufconst:*:)Message':::
GetTypeNameconvert_mnist_siamese_data.cpp(:)( .consttext._ZN6google17MakeCheckOpStringIjjEEPSsRKT_RKT0_PKc'[
_ZN6google17MakeCheckOpStringIjjEEPSsRKT_RKT0_PKc/]usr+/0x43bin)/:ld :undefined  .referencebuild_release /tolib /`libcaffe.sogoogle:: :undefinedbase :reference: CheckOpMessageBuilderto: :`NewStringgoogle(:):'base
:/:usrCheckOpMessageBuilder/:bin:/NewStringld(:) '.
build_release//usrlib//binlibcaffe.so/:ld :undefined  .referencebuild_release /tolib /`libcaffe.sogoogle:: :undefinedprotobuf :reference: Messageto: :`InitializationErrorStringgoogle(:): protobufconst:':
Message/:usr:/DebugStringbin(/)ld :const '.
build_release//usrlib//binlibcaffe.so/:ld :undefined  .referencebuild_release /tolib /`libcaffe.sogoogle:: :undefinedprotobuf :reference: internalto: :`WireFormatLitegoogle::::WriteStringMaybeAliasedprotobuf(:int:,MessageLite :std::ParseFromString:(stringstd :const:&string,  constgoogle&:):'protobuf
:/:usrio/:bin:/CodedOutputStreamld*:) '.
build_release//usrlib//binlibcaffe.so/:ld :undefined  .referencebuild_release /tolib /`libcaffe.sogoogle:: :undefinedprotobuf :reference: internalto: :`NameOfEnumgoogle(:google::protobuf::protobuf::internal::EnumDescriptor: AssignDescriptorsconst(*std,: :intstring) 'const
&/,usr /googlebin:/:ldprotobuf:: :.internalbuild_release:/:libMigrationSchema/ libcaffe.soconst:* ,undefined  googlereference: :toprotobuf :`:googleMessage: :constprotobuf*: :constinternal*:,: WireFormatLiteunsigned: :intReadBytes (constgoogle*:,: protobufgoogle::::ioprotobuf::::CodedInputStreamMetadata**,,  stdgoogle::::stringprotobuf*:):'EnumDescriptor
 /constusr*/*bin,/ ldgoogle:: :.protobufbuild_release:/:libServiceDescriptor/ libcaffe.soconst:* *undefined) 'reference
 /tousr /`bingoogle/:ld::protobuf :.:build_releaseMessageFactory/:lib:/InternalRegisterGeneratedFilelibcaffe.so(:char  undefinedconst *reference,  tovoid  `(google*:):(protobufstd::::iostring: :constCodedOutputStream&:):)WriteStringWithSizeToArray'(
std/:usr:/stringbin /constld&:,  .unsignedbuild_release /charlib*/)libcaffe.so':
 /undefinedusr /referencebin /told :` leveldb.:build_release:/DBlib:/:libcaffe.soOpen:( leveldbundefined: :referenceOptions  toconst &`,google :std::protobuf::string: Messageconst:&:,GetTypeName (leveldb): :constDB'*
*/)usr'/
bin//usrld/:bin /.ldbuild_release:/ lib./build_releaselibcaffe.so/:lib /undefinedlibcaffe.so :reference  undefinedto  reference` googleto: :`protobufgoogle::::Messageprotobuf::::DebugStringinternal(:): WireFormatLiteconst:':
WriteBytesMaybeAliased/(usrint/,bin /stdld::: string. build_releaseconst/&lib,/ libcaffe.sogoogle:: :undefinedprotobuf :reference: ioto: :`CodedOutputStreamgoogle*:):'protobuf
:/:usrMessageLite/:bin:/ParseFromStringld(:std :.:build_releasestring/ libconst/&libcaffe.so):'
undefined/ usrreference/ binto/ ld`:leveldb :.:build_releaseStatus/:lib:/ToStringlibcaffe.so(:)  undefinedconst 'reference
 /tousr /`bingoogle/:ld::protobuf :.:build_releaseinternal/:lib:/NameOfEnumlibcaffe.so(:google :undefined: protobufreference: :toEnumDescriptor  `constgoogle*:,: protobufint:):'internal
:/:usrWireFormatLite/:bin:/WriteStringld(:int ,. build_releasestd/:lib:/stringlibcaffe.so :const &undefined,  referencegoogle :to: protobuf`:google::io::protobuf::CodedOutputStream:*internal):':
WireFormatLite::ReadBytes(google::protobuf::io::CodedInputStream*, std::string*)collect2: error: ld returned 1 exit status
'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::MessageFactory::InternalRegisterGeneratedFile(char const*, void (*)(std::string const&))'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteBytesMaybeAliased(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
/usrmake: *** [Makefile:643：.build_release/examples/cifar10/convert_cifar_data.bin] 错误 1
/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::Status::ToString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteString(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
collect2: error: ld returned 1 exit status
make: *** [Makefile:643：.build_release/examples/siamese/convert_mnist_siamese_data.bin] 错误 1

```

为什么这里始终是高版本的gcc
```
cat /proc/driver/nvidia/version
```

```
ll /usr/bin/gcc*

```

```
sudo ln -s /usr/bin/gcc-4.8* /usr/bin/gcc -f
sudo ln -s /usr/bin/gcc-ar-4.8* /usr/bin/gcc-ar -f
sudo ln -s /usr/bin/gcc-4.8* /usr/bin/gcc.bak -f
sudo ln -s /usr/bin/gcc-nm-4.8* /usr/bin/gcc-nm -f
sudo ln -s /usr/bin/gcc-ranlib-4.8* /usr/bin/gcc-ranlib -f
```

```
sudo ln -s /usr/bin/gcc-9* /usr/bin/gcc -f
sudo ln -s /usr/bin/gcc-ar-9* /usr/bin/gcc-ar -f
sudo ln -s /usr/bin/gcc-9* /usr/bin/gcc.bak -f
sudo ln -s /usr/bin/gcc-nm-9* /usr/bin/gcc-nm -f
sudo ln -s /usr/bin/gcc-ranlib-9* /usr/bin/gcc-ranlib -f
```

```
ll /usr/bin/g++*
```

```
sudo ln -s /usr/bin/g++-4.8* /usr/bin/g++ -f
sudo ln -s /usr/bin/g++-4.8* /usr/bin/g++.bak -f
```
```
sudo ln -s /usr/bin/g++-9* /usr/bin/g++ -f
sudo ln -s /usr/bin/g++-9* /usr/bin/g++.bak -f
```
---

#### 编译

```
sudo make clean
sudo make all -j12
```



---
