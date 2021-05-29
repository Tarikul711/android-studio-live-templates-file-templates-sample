# android-file-template-live-template-sample

## Android live templete for Intent

```java
fun get$PREFIX$Intent(context: Context, $PARAM1$: $DATATYPE1$, $PARAM2$: $DATATYPE2$): Intent {
        Intent(context, $ACTIVITY$::class.java)
        intent.`package` = context.packageName
        intent.putExtra($NAME1$, $PARAM1$)
        intent.putExtra($NAME2$, $PARAM2$)
        return intent
    }
```

## Jetpack all dependency file/live templete

```java
    implementation 'androidx.recyclerview:recyclerview:1.1.0'
    implementation 'com.github.bumptech.glide:glide:4.11.0'
    annotationProcessor 'com.github.bumptech.glide:compiler:4.11.0'

    // liveData-viewModel android jetpack
    implementation 'androidx.lifecycle:lifecycle-common:2.2.0'
    implementation 'androidx.lifecycle:lifecycle-runtime:2.2.0'
    implementation 'android.arch.lifecycle:extensions:2.2.0'
    implementation 'androidx.lifecycle:lifecycle-livedata-ktx:2.2.0'
    implementation 'androidx.lifecycle:lifecycle-viewmodel-ktx:2.2.0'


    //Retrofit
    implementation 'com.squareup.retrofit2:retrofit:2.8.1'
    implementation 'com.google.code.gson:gson:2.8.6'
    implementation 'com.squareup.retrofit2:converter-gson:2.8.1'
    implementation 'com.squareup.okhttp3:logging-interceptor:4.4.0'

    // kotlin Coroutine
    implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.3.9'
    implementation 'androidx.navigation:navigation-fragment-ktx:2.3.0'
    implementation 'androidx.navigation:navigation-ui-ktx:2.3.0'

    // room library
    implementation "androidx.room:room-runtime:2.2.5"
    kapt "androidx.room:room-compiler:2.2.5"
    implementation "androidx.room:room-ktx:2.2.5"
    androidTestImplementation "androidx.room:room-testing:2.2.5"
```

## Android RecyclerView Adapter live template / file template with dynamic data

```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end

import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup

#parse("File Header.java")

class ${NAME} (var items: MutableList<${ITEM_CLASS}>, val itemClick: (${ITEM_CLASS}) -> Unit) : RecyclerView.Adapter<${NAME}.${VIEWHOLDER_CLASS}>() {

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ${VIEWHOLDER_CLASS} {
        val view = LayoutInflater.from(parent.context).inflate(R.layout.${LAYOUT_RES_ID}, parent, false)
        return ${VIEWHOLDER_CLASS}(view, itemClick)
    }

    override fun onBindViewHolder(holder: ${VIEWHOLDER_CLASS}, position: Int) {
        holder.bindView(items[position])
    }

    override fun getItemCount(): Int = items.size

    /*Private Methods - START*/
    fun clear(){
        this.items.clear()
        notifyDataSetChanged()
    }

    fun replaceItems(items: MutableList<${ITEM_CLASS}>){
        this.items.clear()
        this.items = items
        notifyDataSetChanged()
    }

    fun addItem(item: ${ITEM_CLASS}){
        this.items.add(item)
        notifyItemInserted(itemCount)
    }

    fun removeItem(item: ${ITEM_CLASS}) {
        val position: Int? = this.items.indexOf(item)
        position?.let { pos ->
            this.items.removeAt(pos)
            notifyItemRemoved(pos)
        } ?: run {
            Log.e("${NAME}", "Item not found !")
        }
    }
    /*Private Methods - END*/

    class ${VIEWHOLDER_CLASS}(val view: View, val itemClick: (${ITEM_CLASS}) -> Unit) : RecyclerView.ViewHolder(view) {
        // here comes all the views / variables from view.findViewById()
        // Example: val textView = view.findViewById(R.id.textView1)
        fun bindView(item: ${ITEM_CLASS}) {
            with(item) {
                // here you do all kind of assignments and logics..
                // for Example: textView.text = item.name or just name
                itemView.setOnClickListener { itemClick(this) }
            }
        }
    }

}
```

## Android RecyclerView Adapter live template / file template

```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME}#end

import android.support.v7.widget.RecyclerView
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import java.util.*

#parse("File Header.java")
class ${NAME} : RecyclerView.Adapter<${ViewHolder_Class}>() {

    private var data: List<${Model_Class}> = ArrayList()

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ${ViewHolder_Class} {
        return ${ViewHolder_Class}(
            LayoutInflater.from(parent.context)
                    .inflate(R.layout.${Item_Layout_ID}, parent, false)
        )
    }

    override fun getItemCount() = data.size

    override fun onBindViewHolder(holder: ${ViewHolder_Class}, position: Int) = holder.bind(data[position])

    fun swapData(data: List<${Model_Class}>) {
        this.data = data
        notifyDataSetChanged()
    }

    class ${ViewHolder_Class}(itemView: View) : RecyclerView.ViewHolder(itemView) {
        fun bind(item: ${Model_Class}) = with(itemView) {
            // TODO: Bind the data with View
            setOnClickListener {
                // TODO: Handle on click
            }
        }
    }
}
```

## Android RecyclerView Adapter live template / file template with DiffUtil class

```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME}#end

import androidx.recyclerview.widget.RecyclerView
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import androidx.recyclerview.widget.DiffUtil
import java.util.*

#parse("File Header.java")
class ${NAME} : RecyclerView.Adapter<${ViewHolder_Class}>() {

    private var data: List<${Model_Class}> = ArrayList()

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ${ViewHolder_Class} {
        return ${ViewHolder_Class}(
            LayoutInflater.from(parent.context)
                    .inflate(R.layout.${Item_Layout_ID}, parent, false)
        )
    }

    override fun getItemCount() = data.size

    override fun onBindViewHolder(holder: ${ViewHolder_Class}, position: Int) = holder.bind(data[position])

    fun swapData(data: List<${Model_Class}>) {
    val diffUtil =
                RecyclerDiffUtil(this.data, data)
        val diffUtilResult = DiffUtil.calculateDiff(diffUtil)
        this.data = data
        diffUtilResult.dispatchUpdatesTo(this)
    }


    class ${ViewHolder_Class}(itemView: View) : RecyclerView.ViewHolder(itemView) {
        fun bind(item: ${Model_Class}) = with(itemView) {
            // TODO: Bind the data with View
            setOnClickListener {
                // TODO: Handle on click
            }
        }
    }
}
```

## Android Run Time Permission live template / file template

```java
if (ContextCompat.checkSelfPermission(this, $PERMISSION$)
        != PackageManager.PERMISSION_GRANTED) {
    // Permission is not granted
    // Should we show an explanation?
    if (ActivityCompat.shouldShowRequestPermissionRationale(this,
            $PERMISSION$)) {
        TODO("Show Explainantion if needed")
    } else {
        // No explanation needed, we can request the permission.
        ActivityCompat.requestPermissions(this,
                arrayOf($PERMISSION$),
                $REQUESTCODE$)
    }
} else {
    // Permission has already been granted
}
```

## Android Retrofit builder live template / file template

```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME}#end

import okhttp3.*
import okhttp3.logging.HttpLoggingInterceptor
import retrofit2.Retrofit
import retrofit2.converter.gson.GsonConverterFactory
import java.util.concurrent.TimeUnit


#parse("File Header.java")

object RetrofitBuilder {
    private const val BASE_URL = "${api_base_url}"

    // Caching data from online
    var cacheSize: Long = 5 * 1024 * 1024;
    var HEADER_CACHE_CONTROL: String = "Cache-Control"
    var HEADER_PRAGMA: String = "Pragma"


    var httpClient =
        OkHttpClient.Builder()
            .cache(cache())
            .addInterceptor(httpLoggingInterceptor())
            .addNetworkInterceptor(NetworkInterceptor())
            .addInterceptor(OfflineInterceptor())


    private fun getRetrofit(): Retrofit {
        return Retrofit.Builder()
            .baseUrl(BASE_URL)
           .client(httpClient.build())
            .addConverterFactory(GsonConverterFactory.create())
            .build()
    }

    val apiService: ${ApiService} = getRetrofit().create( ${ApiService}::class.java)

    private fun cache(): Cache {
        return Cache(MyApplication.instance.cacheDir, cacheSize)
    }


    private fun httpLoggingInterceptor(): HttpLoggingInterceptor { // will call in the offline mode
        val httpLoggingInterceptor = HttpLoggingInterceptor()
        httpLoggingInterceptor.level = HttpLoggingInterceptor.Level.BODY
        return httpLoggingInterceptor
    }


    class NetworkInterceptor : Interceptor {
        override fun intercept(chain: Interceptor.Chain): Response {
            val response = chain.proceed(chain.request())
            val cacheControl = CacheControl.Builder()
                .maxAge(5, TimeUnit.SECONDS)
                .build()
            return response.newBuilder()
                .removeHeader(HEADER_PRAGMA)
                .removeHeader(HEADER_CACHE_CONTROL)
                .header(HEADER_CACHE_CONTROL, cacheControl.toString())
                .build();
        }
    }

    class OfflineInterceptor : Interceptor {
        override fun intercept(chain: Interceptor.Chain): Response {
            val request = chain.request()

            if (!NetworkUtils.hasNetwork(MyApplication.instance.applicationContext)!!) {
                val cacheControl: CacheControl = CacheControl.Builder()
                    .maxStale(7, TimeUnit.DAYS).build()
                request.newBuilder()
                    .removeHeader(HEADER_PRAGMA)
                    .removeHeader(HEADER_CACHE_CONTROL)
                    .cacheControl(cacheControl)
                    .build();
            }

            return chain.proceed(request)
        }
    }

}
```
