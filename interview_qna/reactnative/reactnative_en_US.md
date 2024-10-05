### **React Native Interview Questions**

---

**Q1. What is React Native, and how does it differ from React?**

- **Answer**:
  React Native is a framework for building mobile applications using React. The main difference from React is that while React is used for web applications, React Native allows developers to create mobile apps that run on both iOS and Android using native components instead of web components. This results in performance closer to native apps.

---

**Q2. What are the core components of React Native?**

- **Answer**:
  Core components of React Native include:
  - **View**: A container that supports layout with flexbox, style, and touch handling.
  - **Text**: Used for displaying text.
  - **Image**: For displaying images in the app.
  - **ScrollView**: A scrolling container that can hold multiple components.
  - **FlatList**: A performant interface for rendering large lists of data.
  - **TouchableOpacity / TouchableHighlight**: Components for handling touch interactions.

---

**Q3. Explain how styling works in React Native.**

- **Answer**:
  Styling in React Native is done using a JavaScript object, where styles are defined in camelCase instead of kebab-case (e.g., `backgroundColor` instead of `background-color`). Styles can be applied using the `StyleSheet.create` method, which optimizes the performance by reducing the number of styles sent to the native side.

  Example:

  ```javascript
  const styles = StyleSheet.create({
    container: {
      flex: 1,
      justifyContent: "center",
      alignItems: "center",
      backgroundColor: "#fff",
    },
  });
  ```

---

**Q4. What is the purpose of the `StyleSheet` API in React Native?**

- **Answer**:
  The `StyleSheet` API in React Native is used to create and manage styles for components. It allows for better performance by batching styles and minimizing the overhead of creating styles directly in components. It also provides a way to define styles in a more structured and reusable manner.

---

**Q5. How do you handle navigation in a React Native application?**

- **Answer**:
  Navigation in React Native can be handled using libraries such as **React Navigation** or **React Native Navigation**. React Navigation is the most commonly used library and provides various navigators like Stack Navigator, Tab Navigator, and Drawer Navigator.

  Example using React Navigation:

  ```javascript
  import { NavigationContainer } from "@react-navigation/native";
  import { createStackNavigator } from "@react-navigation/stack";

  const Stack = createStackNavigator();

  function App() {
    return (
      <NavigationContainer>
        <Stack.Navigator>
          <Stack.Screen name="Home" component={HomeScreen} />
          <Stack.Screen name="Details" component={DetailsScreen} />
        </Stack.Navigator>
      </NavigationContainer>
    );
  }
  ```

---

**Q6. What are the differences between `ScrollView` and `FlatList` in React Native?**

- **Answer**:
  - **ScrollView**: A container that can hold multiple components and allows scrolling. It renders all its children at once, which can lead to performance issues with large datasets.
  - **FlatList**: A performant way to render large lists of data, rendering only the items that are currently visible on the screen. It supports features like item separators, pull-to-refresh, and infinite scrolling.

---

**Q7. Explain how to manage state in a React Native application.**

- **Answer**:
  State management in a React Native application can be handled in several ways:
  - **Local State**: Using React’s built-in `useState` and `useReducer` hooks for component-specific state.
  - **Context API**: For managing global state without prop drilling, allowing components to access shared state.
  - **Redux**: A popular state management library for handling complex state and side effects.
  - **MobX**: An alternative to Redux that allows for more flexible state management using observables.

---

**Q8. What are hooks in React Native, and how are they used?**

- **Answer**:
  Hooks are functions that allow you to use React features in functional components. Commonly used hooks include:

  - **useState**: For managing state in functional components.
  - **useEffect**: For managing side effects like data fetching.
  - **useContext**: For accessing context values.

  Example using `useState`:

  ```javascript
  const [count, setCount] = useState(0);
  ```

---

**Q9. How can you implement authentication in a React Native application?**

- **Answer**:
  Authentication in a React Native application can be implemented using libraries like **Firebase Authentication** or **OAuth**. Common steps include:

  - Set up the authentication provider (e.g., Firebase).
  - Use authentication functions to sign in or sign up users.
  - Store user tokens securely using libraries like `react-native-keychain` or `AsyncStorage`.

  Example with Firebase:

  ```javascript
  import auth from "@react-native-firebase/auth";

  const signIn = async (email, password) => {
    try {
      await auth().signInWithEmailAndPassword(email, password);
    } catch (error) {
      console.error(error);
    }
  };
  ```

---

**Q10. What is the difference between `useEffect` and `componentDidMount` in React Native?**

- **Answer**:
  - **useEffect**: A hook used in functional components that runs after render and can handle side effects. It can run on mount, update, and unmount depending on the dependency array.
  - **componentDidMount**: A lifecycle method in class components that runs only once after the component is first rendered. It is typically used for initiating data fetching or subscriptions.

---

**Q11. How do you optimize performance in a React Native application?**

- **Answer**:
  Performance optimization techniques include:
  - **Use FlatList** instead of ScrollView for large datasets.
  - **Optimize images** by using appropriate formats and sizes.
  - **Avoid unnecessary re-renders** by using memoization techniques (`React.memo`, `useCallback`, `useMemo`).
  - **Use native modules** for heavy computations or animations.
  - **Profile the application** using tools like React Native Performance Monitor to identify bottlenecks.

---

**Q12. How do you implement internationalization (i18n) in a React Native app?**

- **Answer**:
  Internationalization in React Native can be achieved using libraries such as **i18next** or **react-intl**. These libraries help manage translations and locale changes effectively.

  Example using i18next:

  ```javascript
  import i18n from "i18next";
  import { initReactI18next } from "react-i18next";

  i18n.use(initReactI18next).init({
    resources: {
      en: { translation: { welcome: "Welcome" } },
      fr: { translation: { welcome: "Bienvenue" } },
    },
    lng: "en",
    fallbackLng: "en",
  });

  function App() {
    return <Text>{i18n.t("welcome")}</Text>;
  }
  ```

---

**Q13. What are the advantages of using React Native over traditional native development?**

- **Answer**:
  Advantages of React Native include:
  - **Cross-Platform Development**: Write code once and run it on both iOS and Android, reducing development time and costs.
  - **Hot Reloading**: Allows developers to see changes in real-time without recompiling the entire application.
  - **Reusable Components**: Leverage a component-based architecture that promotes code reusability.
  - **Large Ecosystem**: Access to a rich set of libraries and community support for faster development.
  - **JavaScript**: Use a familiar language for web developers, making it easier to transition to mobile development.

---

**Q14. How do you handle permissions in a React Native application?**

- **Answer**:
  Permissions can be handled using the **react-native-permissions** library, which provides a unified API to request and check permissions for various features such as location, camera, and notifications.

  Example:

  ```javascript
  import { check, request, PERMISSIONS } from "react-native-permissions";

  async function requestLocationPermission() {
    const result = await request(PERMISSIONS.ANDROID.ACCESS_FINE_LOCATION);
    if (result === "granted") {
      // Permission granted
    } else {
      // Permission denied
    }
  }
  ```

---

**Q15. What is the role of the React Native CLI, and how does it differ from Expo?**

- **Answer**:
  The React Native CLI is a command-line tool for creating and managing React Native applications. It allows full control over the native code and configuration. Expo, on the other hand, is a framework built on top of React Native that provides a managed workflow with built-in tools and libraries, simplifying development but limiting some native capabilities.

  Key differences:

  - **Development Workflow**: Expo provides an easier setup with a managed workflow, while the React Native CLI allows for full native code access.
  - **Ecosystem**: Expo comes with a wide range of pre-configured APIs (e.g., camera, location) out of the box, while the React Native

CLI requires manual linking and configuration for third-party libraries.

---

**Q16. Explain the concept of bridging in React Native.**

- **Answer**:
  Bridging in React Native allows communication between the JavaScript code and the native platform (iOS/Android). This is essential for calling native APIs or accessing native modules that are not available in React Native.

  The bridge facilitates the exchange of messages and data between the two environments, enabling developers to create custom native modules and integrate them with React Native components.

---

**Q17. How can you handle deep linking in a React Native application?**

- **Answer**:
  Deep linking allows users to navigate directly to specific content within a mobile application from an external link. In React Native, deep linking can be handled using the **React Navigation** library.

  Steps to implement deep linking:

  1. Define the linking configuration in your navigator.
  2. Use URL patterns to specify how to route the app based on incoming URLs.
  3. Configure your mobile app manifest to handle the URL scheme.

  Example:

  ```javascript
  const linking = {
    prefixes: ["https://myapp.com", "myapp://"],
    config: {
      screens: {
        Home: "home",
        Profile: "user/:id",
      },
    },
  };

  <NavigationContainer linking={linking}>
    <Stack.Navigator>
      <Stack.Screen name="Home" component={HomeScreen} />
      <Stack.Screen name="Profile" component={ProfileScreen} />
    </Stack.Navigator>
  </NavigationContainer>;
  ```

---

**Q18. How do you implement push notifications in a React Native application?**

- **Answer**:
  Push notifications in React Native can be implemented using libraries like **react-native-firebase** or **react-native-push-notification**. Common steps include:

  - Set up a backend service to send notifications (e.g., Firebase Cloud Messaging).
  - Configure the app to handle notifications by requesting permissions and handling incoming notifications.

  Example using Firebase:

  ```javascript
  import messaging from "@react-native-firebase/messaging";

  async function requestUserPermission() {
    const authStatus = await messaging().requestPermission();
    const enabled =
      authStatus === messaging.AuthorizationStatus.AUTHORIZED ||
      authStatus === messaging.AuthorizationStatus.PROVISIONAL;

    if (enabled) {
      console.log("Authorization status:", authStatus);
    }
  }
  ```

---

**Q19. What are some common debugging techniques for React Native applications?**

- **Answer**:
  Common debugging techniques include:
  - **React Native Debugger**: A standalone app that combines Chrome DevTools with React DevTools, allowing inspection of component hierarchies, state, and props.
  - **Console Logging**: Using `console.log` to track variable values and application flow.
  - **Remote Debugging**: Enabling remote debugging in the React Native app and using Chrome DevTools for debugging JavaScript code.
  - **Error Boundaries**: Implementing error boundaries to catch and handle errors in components gracefully.

---

**Q20. How do you implement animations in React Native?**

- **Answer**:
  Animations in React Native can be implemented using the **Animated API** or libraries like **React Native Reanimated** and **react-native-animatable**. The Animated API provides a powerful and flexible way to create animations using various animation types (e.g., timing, spring).

  Example using the Animated API:

  ```javascript
  import { Animated } from "react-native";

  function MyComponent() {
    const opacity = useRef(new Animated.Value(0)).current;

    useEffect(() => {
      Animated.timing(opacity, {
        toValue: 1,
        duration: 1000,
        useNativeDriver: true,
      }).start();
    }, [opacity]);

    return (
      <Animated.View style={{ opacity }}>
        <Text>Hello!</Text>
      </Animated.View>
    );
  }
  ```

---

**Q21. How can you test React Native components?**

- **Answer**:
  Testing React Native components can be accomplished using libraries like **Jest** and **React Native Testing Library**. You can write unit tests for component logic, interaction tests for user events, and snapshot tests to verify component rendering.

  Example using React Native Testing Library:

  ```javascript
  import { render, fireEvent } from "@testing-library/react-native";
  import MyComponent from "./MyComponent";

  test("renders correctly and handles button press", () => {
    const { getByText } = render(<MyComponent />);
    fireEvent.press(getByText("Submit"));
    expect(getByText("Submitted!")).toBeTruthy();
  });
  ```

---

**Q22. What is the purpose of `react-native-gesture-handler`, and how is it used?**

- **Answer**:
  `react-native-gesture-handler` is a library that provides a better way to handle gestures in React Native applications, improving touch responsiveness and performance. It replaces the built-in gesture system with a more robust and flexible one.

  Example usage:

  ```javascript
  import {
    GestureHandlerRootView,
    TapGestureHandler,
  } from "react-native-gesture-handler";

  function MyComponent() {
    const onPress = () => {
      console.log("Tapped!");
    };

    return (
      <GestureHandlerRootView>
        <TapGestureHandler onActivated={onPress}>
          <View style={{ width: 200, height: 200, backgroundColor: "blue" }} />
        </TapGestureHandler>
      </GestureHandlerRootView>
    );
  }
  ```

---

**Q23. Explain how to handle accessibility in React Native applications.**

- **Answer**:
  Accessibility in React Native applications can be managed by:
  - Using proper accessibility props (e.g., `accessible`, `accessibilityLabel`, `accessibilityRole`) to provide information to screen readers.
  - Ensuring that all interactive elements are focusable and navigable.
  - Providing meaningful descriptions for images and buttons.
  - Testing with accessibility tools and using the `Accessibility Inspector` in iOS or the `TalkBack` feature in Android to verify that the app is accessible.

---

**Q24. How can you create a responsive layout in React Native?**

- **Answer**:
  To create responsive layouts in React Native, you can use:

  - **Flexbox**: Leverage the Flexbox layout model to create flexible and adaptive designs that adjust to different screen sizes.
  - **Dimensions API**: Use the `Dimensions` API to get the device's screen dimensions and adjust styles accordingly.
  - **Percentage-based widths**: Use percentage values for width and height instead of fixed pixel values to allow components to adapt to various screen sizes.

  Example:

  ```javascript
  import { Dimensions, StyleSheet, View } from "react-native";

  const { width } = Dimensions.get("window");

  const styles = StyleSheet.create({
    container: {
      width: width * 0.8, // 80% of screen width
      height: 200,
    },
  });
  ```

---

**Q25. What is the difference between `AsyncStorage` and `SecureStore` in React Native?**

- **Answer**:

  - **AsyncStorage**: A simple, unencrypted, persistent storage system for key-value pairs. It is suitable for storing non-sensitive data but does not provide security features.
  - **SecureStore**: A storage solution that provides a more secure way to store sensitive data like tokens and passwords. It uses the device's secure storage (Keychain for iOS, Encrypted SharedPreferences for Android) to protect data at rest.

  Example usage of SecureStore:

  ```javascript
  import * as SecureStore from "expo-secure-store";

  const saveData = async (key, value) => {
    await SecureStore.setItemAsync(key, value);
  };
  ```
