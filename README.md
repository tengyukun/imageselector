# imageselector
图片选择器

 [原作者地址](https://github.com/lovetuzitong/MultiImageSelector/blob/master/README_zh.md)
 
 仿微信实现多图选择。支持单选和多选两种模式
 ![](https://github.com/lovetuzitong/MultiImageSelector/blob/master/art/select_1.png)
 ![](https://github.com/lovetuzitong/MultiImageSelector/blob/master/art/example_1.png)
 ![](https://github.com/lovetuzitong/MultiImageSelector/blob/master/art/select_2.png)
 ![](https://github.com/lovetuzitong/MultiImageSelector/blob/master/art/select_3.png)
 
### 运行DEMO

./gradlew installDebug
### 快速开始

#### 第0步 把模块 multi-image-selector 作为你的项目依赖添加到工程中. 在项目build.gradle 中:
    
    
    repositories {
            maven { url "https://jitpack.io" }
    }
    
    dependencies {
        compile 'com.github.lovetuzitong:MultiImageSelector:1.2'
    }
  
#### 第1步 在你的 AndroidManifest.xml 中做如下声明:

    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

    <application

      ...

      <!--Image Selector Entry-->
      <activity
          android:configChanges="orientation|screenSize"
          android:name="me.nereo.multi_image_selector.MultiImageSelectorActivity" />
    </application>
    
#### 第2步 在你的代码中简单调用( 版本version-1.1之后支持 ), eg.

    // Multi image selector form an Activity
    MultiImageSelector.create(Context)
            .start(Activity, REQUEST_IMAGE);

详细可使用的Api.

    MultiImageSelector.create(Context)
            .showCamera(boolean) // 是否显示相机. 默认为显示
            .count(int) // 最大选择图片数量, 默认为9. 只有在选择模式为多选时有效
            .single() // 单选模式
            .multi() // 多选模式, 默认模式;
            .origin(ArrayList<String>) // 默认已选择图片. 只有在选择模式为多选时有效
            .start(Activity/Fragment, REQUEST_IMAGE);

同样支持老版本的 Intent 调用方法:

    Intent intent = new Intent(mContext, MultiImageSelectorActivity.class);
    // 是否显示调用相机拍照
    intent.putExtra(MultiImageSelectorActivity.EXTRA_SHOW_CAMERA, true);
    // 最大图片选择数量
    intent.putExtra(MultiImageSelectorActivity.EXTRA_SELECT_COUNT, 9);
    // 设置模式 (支持 单选/MultiImageSelectorActivity.MODE_SINGLE 或者 多选/MultiImageSelectorActivity.MODE_MULTI)
    intent.putExtra(MultiImageSelectorActivity.EXTRA_SELECT_MODE, MultiImageSelectorActivity.MODE_MULTI);
    // 默认选择图片,回填选项(支持String ArrayList)
    intent.putStringArrayListExtra(MultiImageSelectorActivity.EXTRA_DEFAULT_SELECTED_LIST, defaultDataArray);
    startActivityForResult(intent, REQUEST_IMAGE);

#### 第3步 在你的 onActivityResult 方法中接受结果. 例如:

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if(requestCode == REQUEST_IMAGE){
            if(resultCode == RESULT_OK){
                // 获取返回的图片列表
                List<String> path = data.getStringArrayListExtra(MultiImageSelectorActivity.EXTRA_RESULT);
                // 处理你自己的逻辑 ....
            }
        }
    }
    
#### 第4步 没第4步了，就这样就OK啦~ :)

### 自定义显示

自定义Activity

    class CustomerActivity extends Activity implements MultiImageSelectorFragment.Callback{
     @Override
        protected void onCreate(Bundle savedInstanceState) {
      // 你自己的逻辑...
            Bundle bundle = new Bundle();
            bundle.putInt(MultiImageSelectorFragment.EXTRA_SELECT_COUNT, mDefaultCount);
            bundle.putInt(MultiImageSelectorFragment.EXTRA_SELECT_MODE, mode);
            <bundle class="putBo"></bundle>olean(MultiImageSelectorFragment.EXTRA_SHOW_CAMERA, isShow);
            // 添加主Fragment到Activity
            getSupportFragmentManager().beginTransaction()
                    .add(R.id.image_grid, Fragment.instantiate(this, MultiImageSelectorFragment.class.getName(), bundle))
                    .commit();
     }
     @Override
        public void onSingleImageSelected(String path) {
            // 当选择模式设定为 单选/MODE_SINGLE, 这个方法就会接受到Fragment返回的数据
        }

        @Override
        public void onImageSelected(String path) {
            // 一个图片被选择是触发，这里可以自定义的自己的Actionbar行为
        }

        @Override
        public void onImageUnselected(String path) {
            // 一个图片被反选是触发，这里可以自定义的自己的Actionbar行为
        }

        @Override
        public void onCameraShot(File imageFile) {
            // 当设置了使用摄像头，用户拍照后会返回照片文件
        }
    }
具体可以参考MultiImageSelectorActivity.java的实现

