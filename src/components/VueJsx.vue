<script lang="tsx">
import { defineComponent, reactive, computed } from 'vue'
import { UserOutlined, LockOutlined } from '@ant-design/icons-vue';

export default defineComponent({
  name: 'VueJsx',
  props: {
    msg: {
      type: String,
      default: ''
    }
  },
  setup(props) {
    interface FormState {
      username: string;
      password: string;
      remember: boolean;
    }
    const formState = reactive<FormState>({
      username: '',
      password: '',
      remember: true,
    });
    const onFinish = (values: any) => {
      console.log('Success:', values);
    };

    const onFinishFailed = (errorInfo: any) => {
      console.log('Failed:', errorInfo);
    };
    const rules = {
      username: [
        {
          required: true,
          message: 'Please input your username!',
        }
      ],
      password: [
        {
          required: true,
          message: 'Please input your password!',
        }
      ]
    }
    const disabled = computed(() => {
      return !(formState.username && formState.password);
    });
    return () => {
      if(props.msg) {
        return (
          <a-form
            name="normal_login"
            class="login-form"
            onFinish={onFinish}
            onFinishFailed={onFinishFailed}
          >
            <a-form-item
              label="Username"
              name="username"
              rules={rules.username}
            >
              <a-input v-model={formState.username}>
                <template v-slots:prefix>
                  <UserOutlined class="site-form-item-icon" />
                </template>
              </a-input>
            </a-form-item>

            <a-form-item
              label="Password"
              name="password"
              v-model:rules={rules.password}
            >
              <a-input-password v-model:value={formState.password}>
                <template v-slots:prefix>
                  <LockOutlined class="site-form-item-icon" />
                </template>
              </a-input-password>
            </a-form-item>

            <a-form-item>
              <a-form-item name="remember" no-style>
                <a-checkbox v-model:checked={formState.remember}>Remember me</a-checkbox>
              </a-form-item>
              <a class="login-form-forgot" href="">Forgot password</a>
            </a-form-item>

            <a-form-item>
              <a-button disabled={disabled} type="primary" html-type="submit" class="login-form-button">
                Log in
              </a-button>
              Or
              <a href="">register now!</a>
            </a-form-item>
          </a-form>
        )
      }
    }
  }
})
</script>

<style scoped>
#components-form-demo-normal-login .login-form {
  max-width: 300px;
}
#components-form-demo-normal-login .login-form-forgot {
  float: right;
}
#components-form-demo-normal-login .login-form-button {
  width: 100%;
}
</style>