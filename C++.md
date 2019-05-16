```c++
// 懒汉式 单例模式
class LicenseCheck {
 public:
    static LicenseCheck &
    GetInstance() {
        static LicenseCheck instance;
        return instance;
    };
}
```

