# KotlinListView
Example using Kotlin with a list view for learning 

This example is for classroom learning for triOS Students on how to create a ListView in Kotlin. Using ArrayList.

Code: Main Activity 

    var listView: ListView? = null
    var adapter: UserListAdapter? = null
    ...
      listView = findViewById<ListView>(R.id.listView)
        adapter = UserListAdapter(this, generateData())

        listView?.adapter = adapter
        adapter?.notifyDataSetChanged()
        
        
    ...
      fun generateData(): ArrayList<UserDto> {
        var result = ArrayList<UserDto>()

        for (i in 0..15) { // this will display a range of 15 users with the same name and text
            var user: UserDto = UserDto("Louise ", "Best Teacher ;)")
            result.add(user)
        }

        return result
    }
    
    Code: example UserListAdapter
     create this class
     class UserListAdapter(private var activity: Activity, private var items: ArrayList<UserDto>): BaseAdapter() 
    
     private class ViewHolder(row: View?) {
        var txtName: TextView? = null
        var txtComment: TextView? = null

        init {
            this.txtName = row?.findViewById<TextView>(R.id.txtName)
            this.txtComment = row?.findViewById<TextView>(R.id.txtComment)
        }
    }

    override fun getView(position: Int, convertView: View?, parent: ViewGroup): View {
        val view: View?
        val viewHolder: ViewHolder
        if (convertView == null) {
            val inflater = activity?.getSystemService(Context.LAYOUT_INFLATER_SERVICE) as LayoutInflater
            view = inflater.inflate(R.layout.user_list_row, null)
            viewHolder = ViewHolder(view)
            view?.tag = viewHolder
        } else {
            view = convertView
            viewHolder = view.tag as ViewHolder
        }

        var userDto = items[position]
        viewHolder.txtName?.text = userDto.name
        viewHolder.txtComment?.text = userDto.comment

        return view as View
    }

    override fun getItem(i: Int): UserDto {
        return items[i]
    }

    override fun getItemId(i: Int): Long {
        return i.toLong()
    }

    override fun getCount(): Int {
        return items.size
    }

Code: UserDto

Model Class for User Dto

var name: String = ""
var comment: String = ""

constructor()
  constructor(name: String, comment: String) {
        this.name = name
        this.comment = comment
    }

