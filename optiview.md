# OptiView Real-time Streaming

Dolby OptiView Real-time Streaming is supported in a special HISPlayer SDK "optiview".

Supported Graphics API: **Vulkan**.

To configure OptiView Real-time Streaming, go to HISPlayer multistream properties in Unity editor. Set the following properties as shown below:
- Enable Optiview: Check the checkbox.
- Stream Name: Your Dolby OptiView Real-time stream name.
- Account ID: Your Dolby OptiView Real-time Streaming account ID.

<p align="center">
  <img alt="image" src="https://github.com/user-attachments/assets/a61b6dc0-21ce-4c79-8d8c-ec1c5ee7700b">
</p>

## Related APIs

**class StreamProperties**:
- **public bool enableOptiView**: Checkbox to enable Dolby OptiView Real-time Streaming.
- **public List<string> optiViewStreamName**: List of Dolby OptiView Real-time stream name.
- **public List<string> optiViewAccountId**: List of Dolby OptiView Real-time Streaming account ID.

#### void AddVideoContentOptiViewC(int playerIndex, string streamName, string accountId)
Add new Dolby OptiView Real-time Streaming content to a certain player. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The **streamName** is the Dolby OptiView Real-time stream name. The **accountId** is the account ID associated to Dolby OptiView Real-time Streaming.

#### void ChangeVideoContentOptiView(int playerIndex, string streamName, string accountId)
Change the Dolby OptiView Real-time Streaming content of a certain player to a new stream. The **playerIndex** is associated with the index of the element of **Multi Stream Properties**, e.g. the index 0 is the element 0 in the list. The **streamName** is the Dolby OptiView Real-time stream name. The **accountId** is the account ID associated to Dolby OptiView Real-time Streaming.
