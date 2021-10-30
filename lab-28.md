

## Recycler View on xml file

- Pretty much the container that will display the list of items
- Add RecyclerView to layout
- Grab RecyclerView

## RecyclerViewAdapter

- Need to ask more about what exactly all this does

## Cart Item Fragment

- Is used to inflate the xml file?
- Create `fragments` folder
- Create a new BLANK FRAGMENT

## Models

- Will be ultiamtely used to be put into the recycler View
- Create `models` folder
- Create like any other class with a constructor
- Ctrl Click to generate a to string

## Fragment

- Create RecyclerView on the xml layout that you want
- Configure the fragment
- Right click frame layout
  - Click constrating layout
- Constraint layout id : `fragmentConstaintLayout`
- layout_height: `wrap_content`
- TextView
  id: `currentItemFragmentTextView`
  layout_height: `75dp` is good

- Inflate takes java objects and inflates to a fragment
- Attach a root as false
  - Add child view to parent view LATER = set to FALSE
  - Add child view to parent view LATER = set to TRUE
- Need to make an interface to be able to handle something to be clicked on