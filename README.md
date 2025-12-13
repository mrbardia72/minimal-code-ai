# minimal-code-ai
Token-efficient prompt template for AI code generation. Eliminates boilerplate, documentation, and test files. Production-ready code only.

# 📘 راهنمای کامل پرامپت کدنویسی بهینه

> این راهنما برای کاهش هزینه مصرف توکن و دریافت کد خالص و کاربردی طراحی شده است.

---

## 📋 فهرست مطالب
- [پرامپت اصلی](#پرامپت-اصلی)
- [موارد ممنوع](#موارد-ممنوع)
- [الزامات](#الزامات)
- [قوانین مهم](#قوانین-مهم)
- [استایل کد](#استایل-کد)

---

## 🎯 پرامپت اصلی

```
When generating code, write only the main requested code.

=== FORBIDDEN ===
❌ README files
❌ Tests (unit test, integration test, etc.)
❌ Long explanatory comments
❌ Detailed docstrings
❌ Shell scripts (setup.sh, install.sh, etc.)
❌ Usage examples or demo code
❌ Explanations before or after code
❌ Documentation or guides
❌ Boilerplate code (unless specifically needed)
❌ Logging setup or extensive error messages
❌ Configuration files (unless core functionality)
❌ Docker/container files
❌ CI/CD pipeline files
❌ License files
❌ Changelog or version files
❌ Mock data or fixtures
❌ Migration files (unless specifically requested)

=== REQUIREMENTS ===
✅ Only main functional code
✅ Clear and descriptive variable/function naming
✅ Clean and understandable structure
✅ Production-ready code (not prototype)
✅ Minimal dependencies
✅ Self-contained solution

=== IMPORTANT RULES ===
- Use comments only for complex logic (minimal)
- No messages, greetings, or explanatory text before/after artifact
- Short but meaningful variable names (e.g., userData not u or user_data_information)
- No placeholder comments like "// TODO" or "// Add logic here"
- No print/console.log for debugging (unless it's core feature)
- Assume latest stable version of language/framework
- Don't include import statements for standard library (unless ambiguous)
- No type hints/annotations unless language requires them
- Optimize for readability, not cleverness

=== CODE STYLE ===
- Consistent indentation (tabs for Go)
- One blank line between functions/methods maximum
- No excessive whitespace
- Group related code logically
- Return early to avoid nesting
```

---

## 🚫 موارد ممنوع

### ❌ README files
فایل‌های توضیحاتی پروژه

**مثال چیزی که نمی‌خواهیم:**
```markdown
# My Project
This is a user management system...
```

---

### ❌ Tests
کدهای تست واحد یا یکپارچگی

**مثال بد:**
```go
func TestCreateUser(t *testing.T) {
    user := CreateUser("Ali", 25)
    if user.Name != "Ali" {
        t.Error("Expected Ali")
    }
}
```

---

### ❌ Long explanatory comments
کامنت‌های توضیحی طولانی

**مثال بد:**
```go
// این تابع یک کاربر جدید ایجاد می‌کند
// ابتدا اعتبارسنجی انجام می‌دهد
// سپس کاربر را در دیتابیس ذخیره می‌کند
// و در نهایت شناسه کاربر را برمی‌گرداند
func CreateUser(name string, age int) (*User, error) {
```

**مثال خوب:**
```go
func CreateUser(name string, age int) (*User, error) {
```

---

### ❌ Detailed docstrings
توضیحات کامل توابع

**مثال بد:**
```go
// CreateUser creates a new user in the system
// 
// Parameters:
//   name: The user's full name
//   age: The user's age in years
//
// Returns:
//   *User: Pointer to created user
//   error: Error if validation fails
func CreateUser(name string, age int) (*User, error) {
```

**مثال خوب:**
```go
func CreateUser(name string, age int) (*User, error) {
```

---

### ❌ Shell scripts
اسکریپت‌های نصب و راه‌اندازی

**مثال:**
```bash
#!/bin/bash
go build -o app
./app
```

---

### ❌ Usage examples
نمونه کدهای استفاده

**مثال بد:**
```go
// Example:
//   user, err := CreateUser("Ali", 25)
//   if err != nil {
//       log.Fatal(err)
//   }
func CreateUser(name string, age int) (*User, error) {
```

---

### ❌ Boilerplate code
کدهای تکراری و استاندارد (مگر واقعاً لازم باشد)

**مثال (فقط در صورت لزوم):**
```go
func main() {
    // کد اصلی
}
```

---

### ❌ Logging setup
تنظیمات سیستم لاگ

**مثال بد:**
```go
var log *logrus.Logger

func init() {
    log = logrus.New()
    log.SetFormatter(&logrus.JSONFormatter{})
    log.SetLevel(logrus.InfoLevel)
}
```

---

### ❌ Configuration files
فایل‌های پیکربندی (مگر اینکه خود config قسمت اصلی باشد)

**مثال:**
```json
{
  "database": {
    "host": "localhost",
    "port": 5432
  }
}
```

---

### ❌ Docker/Container files
**مثال:**
```dockerfile
FROM golang:1.21
WORKDIR /app
COPY . .
RUN go build
```

---

### ❌ CI/CD pipeline files
**مثال:**
```yaml
# .github/workflows/test.yml
name: Test
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
```

---

### ❌ Mock data or fixtures
داده‌های تستی ساختگی

**مثال بد:**
```go
var testUsers = []User{
    {Name: "Ali", Age: 25},
    {Name: "Sara", Age: 30},
    {Name: "Reza", Age: 28},
}
```

---

### ❌ Migration files
فایل‌های مهاجرت دیتابیس

**مثال:**
```sql
-- 001_create_users_table.sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);
```

---

## ✅ الزامات

### ✅ Only main functional code
فقط کد اصلی و کاربردی

**مثال خوب:**
```go
type User struct {
    Name string
    Age  int
}

func CreateUser(name string, age int) *User {
    return &User{Name: name, Age: age}
}
```

---

### ✅ Clear and descriptive naming
نام‌گذاری واضح و توصیفی

**مثال‌های خوب:**
```go
userName       // نه u یا n
totalPrice     // نه tp یا price1
isActive       // نه flag یا status
fetchUserData  // نه get یا getData
```

**مثال‌های بد:**
```go
x              // خیلی مبهم
temp           // موقت چیه؟
data1          // چه داده‌ای؟
user_data_info // خیلی طولانی
```

---

### ✅ Clean and understandable structure
ساختار تمیز و قابل فهم

**مثال خوب:**
```go
type UserService struct {
    db Database
}

func (s *UserService) Create(name string) error {
    if name == "" {
        return errors.New("name required")
    }
    return s.db.Insert(name)
}

func (s *UserService) GetAll() ([]User, error) {
    return s.db.Query()
}
```

---

### ✅ Production-ready code
کد آماده استفاده واقعی (نه نمونه)

**مثال بد (نمونه):**
```go
func ProcessPayment(amount float64) {
    // TODO: implement payment logic
    fmt.Println("Payment processed")
}
```

**مثال خوب (آماده تولید):**
```go
func ProcessPayment(amount float64) error {
    if amount <= 0 {
        return errors.New("invalid amount")
    }
    
    transaction := &Transaction{
        Amount: amount,
        Time:   time.Now(),
    }
    
    return transaction.Save()
}
```

---

### ✅ Minimal dependencies
حداقل وابستگی‌ها

**مثال بد:**
```go
import (
    "github.com/pkg1/helper"
    "github.com/pkg2/utils"
    "github.com/pkg3/tools"
    "github.com/pkg4/extras"
)
```

**مثال خوب (استفاده از کتابخانه استاندارد):**
```go
import (
    "fmt"
    "time"
    "errors"
)
```

---

### ✅ Self-contained solution
راه‌حل مستقل

**یعنی:** کد باید بدون وابستگی به فایل‌های خارجی کار کند

```go
// همه چیز در یک فایل (یا چند فایل مرتبط)
type User struct { ... }
func CreateUser() { ... }
func SaveUser() { ... }
```

---

## 🎯 قوانین مهم

### No placeholder comments
بدون کامنت‌های جای‌خالی

**مثال بد:**
```go
func ProcessOrder(order Order) error {
    // TODO: validate order
    // TODO: calculate total
    // TODO: save to database
    return nil
}
```

**مثال خوب:**
```go
func ProcessOrder(order Order) error {
    if err := order.Validate(); err != nil {
        return err
    }
    
    total := order.CalculateTotal()
    return order.Save(total)
}
```

---

### No debugging prints
بدون چاپ‌های دیباگ (مگر اینکه ویژگی اصلی باشد)

**مثال بد:**
```go
func CalculateDiscount(price float64) float64 {
    fmt.Println("Debug: price =", price)
    discount := price * 0.1
    fmt.Println("Debug: discount =", discount)
    return discount
}
```

**مثال خوب:**
```go
func CalculateDiscount(price float64) float64 {
    return price * 0.1
}
```

**استثنا (چاپ به عنوان ویژگی):**
```go
func ShowUserInfo(user User) {
    fmt.Printf("User: %s, Age: %d\n", user.Name, user.Age)
}
```

---

### Short but meaningful names
نام‌های کوتاه اما معنادار

**طیف نام‌گذاری:**
```go
// خیلی کوتاه ❌
u := getUser()

// ایده‌آل ✅
user := getUser()
userData := fetchUserData()

// خیلی طولانی ❌
userDataInformationObject := getUserInfo()
```

---

### Assume latest stable version
فرض کن از آخرین نسخه پایدار استفاده می‌شود

```go
// نیازی به کد قدیمی برای سازگاری نیست
// از ویژگی‌های جدید Go استفاده کن

// Go 1.21+
func Max(a, b int) int {
    return max(a, b) // استفاده از تابع built-in جدید
}
```

---

### Optimize for readability, not cleverness
خوانایی مهم‌تر از باحال بودن کد است

**مثال بد (باحال ولی نامفهوم):**
```go
func IsPrime(n int) bool {
    return n > 1 && func() bool {
        for i := 2; i*i <= n; i++ {
            if n%i == 0 {
                return false
            }
        }
        return true
    }()
}
```

**مثال خوب (ساده و واضح):**
```go
func IsPrime(n int) bool {
    if n <= 1 {
        return false
    }
    
    for i := 2; i*i <= n; i++ {
        if n%i == 0 {
            return false
        }
    }
    
    return true
}
```

---

## 📏 استایل کد

### Consistent indentation
تورفتگی یکنواخت (Go از tabs استفاده می‌کند)

```go
// Go خودکار از tabs استفاده می‌کند
func Example() {
	if true {
		// کد
	}
}
```

---

### One blank line between functions
حداکثر یک خط خالی بین توابع

**مثال بد:**
```go
func Function1() {
}



func Function2() {
}
```

**مثال خوب:**
```go
func Function1() {
}

func Function2() {
}
```

---

### No excessive whitespace
بدون فضای خالی اضافی

**مثال بد:**
```go
x  :=  5
result  :=  calculate( a , b )
```

**مثال خوب:**
```go
x := 5
result := calculate(a, b)
```

---

### Group related code logically
گروه‌بندی منطقی کدهای مرتبط

**مثال خوب:**
```go
type User struct {
    ID   int
    Name string
}

type Order struct {
    ID     int
    UserID int
}

// توابع مرتبط با User
func CreateUser() {}
func DeleteUser() {}

// توابع مرتبط با Order
func CreateOrder() {}
func DeleteOrder() {}
```

---

### Return early to avoid nesting
برگشت زودهنگام برای جلوگیری از تو در تو

**مثال بد (تو در تو زیاد):**
```go
func ValidateUser(user *User) error {
    if user != nil {
        if user.Name != "" {
            if user.Age > 0 {
                if user.Email != "" {
                    return nil
                }
            }
        }
    }
    return errors.New("invalid user")
}
```

**مثال خوب (return زودهنگام):**
```go
func ValidateUser(user *User) error {
    if user == nil {
        return errors.New("user is nil")
    }
    
    if user.Name == "" {
        return errors.New("name is empty")
    }
    
    if user.Age <= 0 {
        return errors.New("invalid age")
    }
    
    if user.Email == "" {
        return errors.New("email is empty")
    }
    
    return nil
}
```

---

## 🎓 مثال کامل

### درخواست:
"یک API ساده برای مدیریت کاربران بنویس"

### خروجی صحیح:

```go
package main

import (
	"encoding/json"
	"net/http"
	"sync"
)

type User struct {
	ID   int    `json:"id"`
	Name string `json:"name"`
	Age  int    `json:"age"`
}

type UserStore struct {
	mu    sync.RWMutex
	users map[int]*User
	nextID int
}

func NewUserStore() *UserStore {
	return &UserStore{
		users: make(map[int]*User),
		nextID: 1,
	}
}

func (s *UserStore) Create(name string, age int) *User {
	s.mu.Lock()
	defer s.mu.Unlock()
	
	user := &User{
		ID:   s.nextID,
		Name: name,
		Age:  age,
	}
	s.users[s.nextID] = user
	s.nextID++
	
	return user
}

func (s *UserStore) Get(id int) (*User, bool) {
	s.mu.RLock()
	defer s.mu.RUnlock()
	
	user, exists := s.users[id]
	return user, exists
}

func (s *UserStore) HandleCreate(w http.ResponseWriter, r *http.Request) {
	var req struct {
		Name string `json:"name"`
		Age  int    `json:"age"`
	}
	
	if err := json.NewDecoder(r.Body).Decode(&req); err != nil {
		http.Error(w, err.Error(), http.StatusBadRequest)
		return
	}
	
	user := s.Create(req.Name, req.Age)
	json.NewEncoder(w).Encode(user)
}

func main() {
	store := NewUserStore()
	
	http.HandleFunc("/users", store.HandleCreate)
	http.ListenAndServe(":8080", nil)
}
```

### چرا این خروجی صحیح است؟
✅ فقط کد اصلی  
✅ بدون README، تست، یا Docker  
✅ نام‌گذاری واضح  
✅ ساختار تمیز  
✅ آماده استفاده  
✅ بدون کامنت اضافی  

---

## 📌 خلاصه

این پرامپت برای:
- ✅ کاهش هزینه توکن
- ✅ دریافت کد خالص و کاربردی
- ✅ حذف محتوای غیرضروری
- ✅ کد production-ready

**نکته:** این پرامپت را در ابتدای مکالمه با AI استفاده کنید یا در تنظیمات Custom Instructions ذخیره کنید.

---

## 🔗 منابع بیشتر

- [Go Style Guide](https://go.dev/doc/effective_go)
- [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)

---

**نسخه:** 1.0  
**زبان:** Golang  
**به‌روزرسانی:** 2024
