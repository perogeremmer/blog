## Answer

```kotlin
import android.content.Intent
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.os.PersistableBundle
import android.widget.Button
import android.widget.EditText
import android.widget.TextView
import android.widget.Toast

class MainActivity : AppCompatActivity() {

    lateinit var btnSubmit : Button
    lateinit var etName : EditText
    lateinit var txtName : TextView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        btnSubmit = findViewById(R.id.btn_submit)
        etName = findViewById(R.id.et_name)
        txtName = findViewById(R.id.txt_name)
        
        btnSubmit.setOnClickListener {
            if (etName.text.isEmpty()) {
                Toast.makeText(
                    applicationContext,
                    "Harap isi nama terlebih dahulu",
                    Toast.LENGTH_SHORT
                ).show()
                return@setOnClickListener
            }

            val intent = Intent(this, SecondActivity::class.java)
            intent.putExtra("result", etName.text.toString())
            startActivity(intent)
        }
    }

    override fun onResume() {
        super.onResume()
        etName.text = null
    }
}
```

<br />

Gunakan fungsi onResume, menurut kitab suci android studio:

> [!NOTE]
> 💡 When the activity enters the Resumed state, it comes to the foreground, and then the system invokes the `[onResume()](https://developer.android.com/reference/android/app/Activity#onResume())` callback. This is the state in which the app interacts with the user. The app stays in this state until something happens to take focus away from the app. Such an event might be, for instance, receiving a phone call, the user’s navigating to another activity, or the device screen’s turning off.

## Artinya

Ketika activity balik ke state resume, sebenernya itu balik ke background, dan sistemnya munculin onResume callback. Ini artinya adalah state dimana aplikasi berinteraksi dengan user. 

Aplikasinya bertahan pada state ini hingga sesuatu terjadi untuk mengambil fokus dari aplikasi, contohnya kejadian untuk instance menerima telfon, **pengguna berpindah dari aktivitas lain**, atau layar perangkat mati.