# Builder模式简单实例

``` 
@Data
class BuilderTarget{

    private final String arg1;

    private final String arg2;

    private final String arg3;

    /**
     * 构建不可变对象
     * @param builder
     */
   private BuilderTarget(Builder builder) {
        this.arg1 = builder.arg1;
        this.arg2 = builder.arg2;
        this.arg3 = builder.arg3;
    }


    public static class Builder{

    private  String arg1;
    private  String arg2;
    private  String arg3;

    Builder addArg1(String arg1) {
        this.arg1 = arg1;
        return this;
    }

    Builder addArg2(String arg2) {
        this.arg2 = arg2;
        return this;
    }

    Builder addArg3(String arg3) {
        this.arg3 = arg3;
        return this;
    }

    BuilderTarget build() {
       return new BuilderTarget(this);
    }

}

    public static void main(String[] args) {
        BuilderTarget.Builder builder = new BuilderTarget.Builder();
        BuilderTarget builderTarget = builder.addArg1("haha")
                                             .addArg2("ni")
                                             .addArg3("hao")
                                             .build();

        System.out.println(builderTarget.toString());
    }

}


```

优点
- 可构建不可变对象，对象状态安全
- 构建时数据清晰
