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