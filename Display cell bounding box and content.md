import os
import pya

# layout file
file_str = r'C:\test_layout.oas'
os.chdir(os.path.dirname(file_str))

# create directory for exported images
script_file = os.path.splitext(file_str)[0]
export_folder = script_file + '_images'
os.makedirs(export_folder, exist_ok=True)

# get main window object and load layout file
mw = pya.Application.instance().main_window()
cell_view = mw.load_layout(file_str, 0)

# get layout view and cell view object
lay_view = mw.current_view()
cell_view_ind = lay_view.active_cellview_index()
layout = cell_view.layout()

for c in layout.each_cell():
  # only export images of cells whose name contains '_unit_cell'
  if '_unit_cell' in c.name:
    # set layout view to display cell
    lay_view.select_cell(c.cell_index(), cell_view_ind)
    w = c.bbox().width()
    h = c.bbox().height()
    lay_view.max_hier()

    # get cell bounding box and set layout view
    box = c.bbox()
    new_box = pya.DBox(box.left/1000, box.bottom/1000, box.right/2000, box.top/1000)
    lay_view.zoom_box(new_box)

    # export image
    res = 2000
    image_file =  export_folder + '\\' + c.name + '.png'
    lay_view.save_image(image_file, res, 8*int(res*(h/w)))
