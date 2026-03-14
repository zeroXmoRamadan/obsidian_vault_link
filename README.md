It serves as the central hub for displaying, managing, and interacting with the user's to-do items. This file implements a fully-featured task management interface with **CRUD operations**, **search functionality**, **sorting options**, and a **tutorial overlay** for new users.

---

## Key Components

### 1. **SortOption Enum**

Defines the available sorting options for the todo list.

dart

enum SortOption {

  createdDate,

  dueDate,

  priority;

  String get displayName {

    switch (this) {

      case SortOption.createdDate:

        return 'Created Date';

      case SortOption.dueDate:

        return 'Due Date';

      case SortOption.priority:

        return 'Priority';

    }

  }

}

---

### 2. **State Management**

The screen uses a 

```
StatefulWidget
```

 to manage the todo list, filtering, and loading state:

dart

class _TodoListScreenState extends State<TodoListScreen> {

  final TodoStorage _storage = TodoStorage();

  List<Todo> _todos = [];

  List<Todo> _filteredTodos = [];

  String _searchQuery = '';

  SortOption _sortOption = SortOption.createdDate;

  bool _isLoading = true;

---

### 3. **Loading & Persisting Todos**

Tasks are loaded from local storage during initialization and saved whenever changes occur:

dart

Future<void> _loadTodos() async {

  setState(() => _isLoading = true);

  final todos = await _storage.loadTodos();

  setState(() {

    _todos = todos;

    _applyFiltersAndSort();

    _isLoading = false;

  });

}

Future<void> _saveTodos() async {

  await _storage.saveTodos(_todos);

  setState(() {

    _applyFiltersAndSort();

  });

}

---

### 4. **Filtering & Sorting Logic**

The 

_applyFiltersAndSort() method handles both search filtering and sorting based on the selected option:

dart

void _applyFiltersAndSort() {

  // Filter by search query

  _filteredTodos = _todos.where((todo) {

    final query = _searchQuery.toLowerCase();

    return todo.title.toLowerCase().contains(query) ||

        todo.description.toLowerCase().contains(query);

  }).toList();

  // Sort based on selected option

  switch (_sortOption) {

    case SortOption.priority:

      _filteredTodos.sort(

        (a, b) => a.priority.sortOrder.compareTo(b.priority.sortOrder),

      );

      break;

    // ... other sort cases

  }

}

---

### 5. **CRUD Operations**

The screen provides complete task management capabilities:

|Operation|Method|Description|
|---|---|---|
|**Create**|_addTodo()|Opens <br><br>```<br>AddTodoDialog<br>```<br><br> and adds the new task|
|**Read**|_loadTodos()|Loads all todos from <br><br>```<br>TodoStorage<br>```|
|**Update**|_editTodo() / <br><br>_toggleTodo()|Edits task or toggles completion status|
|**Delete**|_deleteTodo()|Removes a task from the list|

**Example - Toggle Task Completion:**

dart

void _toggleTodo(Todo todo) {

  setState(() {

    final index = _todos.indexWhere((t) => t.id == todo.id);

    if (index != -1) {

      _todos[index] = todo.copyWith(isCompleted: !todo.isCompleted);

    }

  });

  _saveTodos();

}

---

### 6. **UI Structure**

The build method constructs a 

```
Scaffold
```

 with:

- **AppBar** with a progress counter (
    
    ```
    X of Y completed
    ```
    
    ), settings, and sort buttons
- **Search TextField** with dark mode support
- **ListView** for displaying todos using 
    
    ```
    TodoItemWidget
    ```
    
- **FloatingActionButton** for adding new tasks
- **Tutorial overlay** using the 
    
    ```
    Consumer<TutorialService>
    ```
    

**Example - Search Bar with Dark Mode Styling:**

dart

TextField(

  onChanged: _onSearchChanged,

  decoration: InputDecoration(

    hintText: 'Search todos...',

    prefixIcon: Icon(Icons.search),

    filled: true,

    fillColor: Theme.of(context).brightness == Brightness.dark

        ? const Color(0xFF1C1C2E)

        : Colors.grey[100],

  ),

)

---

### 7. **Tutorial Overlay**

A first-time user tutorial that shows how to delete tasks:

dart

Consumer<TutorialService>(

  builder: (context, tutorialService, child) {

    if (tutorialService.isInitialized &&

        !tutorialService.hasSeenDeleteTutorial &&

        _todos.isNotEmpty) {

      return DeleteTaskTutorialOverlay(

        onDismiss: () => tutorialService.markDeleteTutorialAsSeen(),

      );

    }

    return const SizedBox.shrink();

  },

)

---

## Dependencies

This file imports and uses:

- **Provider** for state management (
    
    ```
    Consumer<TutorialService>
    ```
    
    )
- **TodoStorage** for local persistence
- **ThemeService** for dark/light mode awareness
- Custom widgets: 
    
    ```
    TodoItemWidget
    ```
    
    , 
    
    ```
    AddTodoDialog
    ```
    
    , 
    
    ```
    DeleteTaskTutorialOverlay
    ```
    

---

## Summary Table

|Feature|Implementation|
|---|---|
|**Search**|Real-time filtering by title and description|
|**Sorting**|By created date, due date, or priority|
|**Persistence**|Async load/save via <br><br>```<br>TodoStorage<br>```|
|**Dark Mode**|Conditional styling throughout the UI|
|**Tutorial**|First-time delete task tutorial overlay|
|**Accessibility**|Tooltips on action buttons|