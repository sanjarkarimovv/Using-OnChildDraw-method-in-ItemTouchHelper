    override fun onChildDraw(
        c: Canvas,
        recyclerView: RecyclerView,
        viewHolder: RecyclerView.ViewHolder,
        dX: Float,
        dY: Float,
        actionState: Int,
        isCurrentlyActive: Boolean
    ) {
       val ourViewHolder =
            viewHolder as TodoAdapter.TodoViewHolder 
        val itemView = ourViewHolder.itemView
        val itemViewHeight = itemView.bottom - itemView.top
        val background = ColorDrawable()
        when {
            dX >= 0 -> {
                background.color = Color.GREEN
                background.setBounds(
                    itemView.left, itemView.top, itemView.left + dX.toInt(), itemView.bottom
                )
            }

            dX <= 0 -> {
                background.color = Color.RED
                background.setBounds(
                    itemView.right + dX.toInt(), itemView.top, itemView.right, itemView.bottom
                )
            }
        }

        background.draw(c)

        when {
            dX <= 0 -> {
                // endi delete icon set qilishni ham o'rganamiz
                val deleteIcon = ContextCompat.getDrawable(context, R.drawable.ic_delete_white_24)
                val intrinsicWidth = deleteIcon?.intrinsicWidth ?: -1
                val intrinsicHeight = deleteIcon?.intrinsicHeight ?: -1


                // Calculate position of delete icon
                // For Right Position
                val deleteIconTop = itemView.top + (itemViewHeight - intrinsicHeight) / 2
                val deleteIconMargin = (itemViewHeight - intrinsicHeight) / 2
                val deleteIconLeft = itemView.right - deleteIconMargin - intrinsicWidth
                val deleteIconRight = itemView.right - deleteIconMargin
                val deleteIconBottom = deleteIconTop + intrinsicHeight

                // Draw the delete icon
                deleteIcon?.setBounds(
                    deleteIconLeft, deleteIconTop, deleteIconRight, deleteIconBottom
                )
                deleteIcon?.draw(c)
            }

            dX >= 0 -> {
                val editIcon = ContextCompat.getDrawable(context, R.drawable.baseline_edit_24)
                val intrinsicWidthEdit = editIcon?.intrinsicWidth ?: -1
                val intrinsicHeightEdit = editIcon?.intrinsicHeight ?: -1
                // Calculate position of edit icon
                // For left Position
                val deleteIconTopEdit = itemView.top + (itemViewHeight - intrinsicHeightEdit) / 2
                val deleteIconMarginEdit = (itemViewHeight - intrinsicHeightEdit) / 2
                val deleteIconLeftEdit = itemView.left + deleteIconMarginEdit
                val deleteIconRightEdit = deleteIconLeftEdit + intrinsicWidthEdit
                val deleteIconBottomEdit = deleteIconTopEdit + intrinsicHeightEdit

                // Draw the edit icon
                editIcon?.setBounds(
                    deleteIconLeftEdit, deleteIconTopEdit, deleteIconRightEdit, deleteIconBottomEdit
                )
                editIcon?.draw(c)
            }
        }
        super.onChildDraw(c, recyclerView, viewHolder, dX, dY, actionState, isCurrentlyActive)
    }
