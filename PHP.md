
# Project Title

A brief description of what this project does and who it's for
লারাভেল রিকুয়েস্ট ভ্যালিডেশন


```php

<?php
public function save(Request $request)
{
    
    $messages = array(
        'category_name.required' => 'Category Name should not be empty...',
        'category_name.min' => 'Category Name should be minimum 3 characters...',
        'category_description.required' => 'Category Description should not be empty...',
        'publication_status.required' => 'Choose Publication Status from select option...',

    );

    //This rule will validate data coming from form
    $rules = array(
        'name' => 'required|min:3',
        'description' => 'required'
    );

    //validating data which are coming from form
    $validator = Validator::make($request->all(),$rules,$messages);

   if ($validator->fails()) {
        return redirect()->back()->withInput()->withErrors($validator);
    } else {

        Category::create([
            'category_name' => $request->category_name,
            'category_description' => $request->category_description,
            'publication_status' => $request->publication_status,
            
        ]);
        Session::put('message', 'Save Category Information Successfully !');
        return redirect()->route('route.name');
    }
?>
```